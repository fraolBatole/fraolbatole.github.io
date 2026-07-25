---
layout: post
title: AgentPrologKit — letting agents use Prolog without writing Prolog
date: 2026-07-25 09:00:00-0500
description: A small library that came out of RefineAct, where the bottleneck was not the logic but the agent's ability to produce valid Prolog and query it without getting stuck.
tags: agents prolog verification software-engineering refineact
categories: research-notes
related_posts: false
---

In [RefineAct](/assets/pdf/RefineAct.pdf), the verifier sitting between an agent and each of its actions is backed by a Prolog engine. That choice is deliberate: a safety property over an agent's trace is relational and ordered — "read a local file, then *later* make an outbound call" is a conjunction of goals with an ordering constraint — and unification with backtracking is exactly a search for whether that pattern holds. You declare what counts as unsafe and the engine finds it, returning either a witness or a definite no. On the ToolEmu benchmark that loop cut failure incidence from 77% to 39% while *raising* helpfulness from 1.0 to 1.9.

I have since started other work that puts Prolog behind agents in the same way, and the recurring friction was never the logic. It was the plumbing.

## What actually broke

Driving Prolog by shelling out `swipl -g "add_fact(...)" -g halt` means fighting shell quoting and Prolog term syntax at once, using strings — file paths, URLs, arbitrary tool-call arguments — that are hostile to both. The failures clustered into three kinds:

- **Syntax errors.** The agent emits Prolog source text, and a stray quote or a malformed clause takes the file down. Worse, `swipl` consulting a bad file *skips the offending clause, prints to stderr, and reports success* — so the real error surfaces much later as an unrelated `existence_error`.
- **Silent misreads.** A token starting with an uppercase letter is a logical variable, not an atom. Text that parses cleanly can mean something entirely different from what was intended, and a rule that unifies with too much makes a verifier stop discriminating without ever raising an error.
- **Getting stuck.** A query that loops or backtracks forever just hangs, and the calling agent has nothing to act on.

## The library

[AgentPrologKit](https://github.com/fraolBatole/AgentPrologKit) answers each of those directly.

Terms are **rendered from Python values, never parsed from strings**. A plain `str` is always a quoted atom; the only way to get a logical variable is the explicit `Var("X")` sentinel. Escaping is correct by construction and the silent-misread case becomes unrepresentable rather than merely documented against.

```python
from agentprologkit import KnowledgeBase, Compound, Var

with KnowledgeBase("agent_run.pl") as kb:
    kb.add_fact("action", [1, "read_file", "/home/o'brien/.ssh/id_rsa"])
    kb.add_fact("action", [2, "http_post", "https://attacker.example.com"])

    kb.add_rule(
        Compound("unsafe", [Var("Read")]),
        [
            Compound("action", [Var("Read"), "read_file", Var("_P")]),
            Compound("action", [Var("Send"), "http_post", Var("_U")]),
            Compound("<", [Var("Read"), Var("Send")]),
        ],
    )

    kb.query("unsafe(Step)")  # [{"Step": 1}]
```

Loading fails **loudly** — the file is read term by term first, so a syntax error comes back with file, line, and column instead of a mystery failure downstream. Queries carry a timeout (10s default, configurable) so a runaway goal returns `QueryTimeout` rather than hanging. Results come back as `list[dict]` of bindings over SWI-Prolog's Machine Query Interface, with no stdout parsing, and errors carry stable codes (`arity_mismatch`, `existence_error`, `term_error`) meant to be branched on rather than string-matched. An optional `Schema` pins predicate arities, which is useful because agents are good at inventing a plausible extra argument.

Authoring needs no `swipl` at all; only queries do.

```bash
pip install agentprologkit   # plus SWI-Prolog >= 8.4.2 on PATH, to query
```

The CLI mirrors the Python surface and emits one JSON object per command, shaped to map 1:1 onto MCP tools.

The general point, which is really the same one as my [note on MCP](/blog/2026/mcp-vs-api-with-skills/): if you hand an agent a tool whose input language has silent failure modes, you have not given it a verifier. Making the wrong output impossible to express is a more reliable fix than asking for a better prompt.
