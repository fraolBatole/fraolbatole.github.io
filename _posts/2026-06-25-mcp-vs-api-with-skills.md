---
layout: post
title: Why I stopped treating MCP as just another API wrapper
date: 2026-06-25 09:00:00-0500
description: Six months building with MCP changed how I think about the debate. The question is not API versus MCP. It is whether you want a contract or a prayer.
tags: mcp agents software-engineering
categories: research-notes
related_posts: false
---

There is a recurring argument online these days. One camp says MCP is just a thin wrapper and APIs are fine if you write good skills. The other says MCP is the future of agent tooling. After six months working on a research project that involves MCP, I think both camps are missing the actual point.

The question is not which one wins. The question is what you are building against when you use each one.

## Skills are documentation, not contracts

When you bolt a skill onto an API, you are writing a human-readable description of what the API does and hoping an agent reads it correctly. The skill has no binding relationship to the actual API behavior. It is a note. The agent can misread it, invent parameters that do not exist, or miss an edge case the skill author did not think to mention.

I watched this happen on a small project before I switched to MCP. The agent kept making the same class of mistake on a nested parameter. The skill described the structure, but the description was not tight enough, and the agent filled in the gap with its best guess. Right intent, wrong shape, silent failure.

MCP changes the ground rule. The schema is the contract. The tool definition, its parameters, and the error responses are machine-consumable by design. The agent is not interpreting a description. It is reading a spec that was written to be read by machines. That shift sounds small. It is not.

## Developers build differently when a spec exists

This one surprised me. When you build an MCP server, you are forced to think carefully about what your tool actually does, what parameters are required versus optional, and what failure looks like at the boundary. That discipline produces better tools.

Compare that to adding a skill. The incentive there is to describe just enough to make the agent probably work. There is no formal feedback loop telling you your description was ambiguous. The agent tries, fails in some subtle way, and you patch the skill with more text. Then more text. Then a disclaimer.

MCP developers are more cautious not because they are more careful people, but because the format demands it. The spec enforces precision that a prose description never will.

## You can actually find what is available

One thing I did not expect to matter as much as it does is discoverability. With an API and a set of skills, finding the right tool for a specific job is a problem the agent has to solve through prose. It reads descriptions, guesses which skill is relevant, and sometimes picks the wrong one.

MCP servers expose their tools in a structured, enumerable format. An agent can ask what tools exist, read their signatures, and reason about which one fits without guessing whether a skill even exists for this case. It is a smaller thing, but in a system with many tools spread across many servers, it starts to matter a lot.

## Errors that actually help

APIs return errors designed for developers who will read them, add logging, and figure out what went wrong. That is fine for a human. An agent needs something different.

MCP errors are part of the protocol. When something goes wrong in an MCP call, the response is structured in a way that tells the agent what happened and where. That closes a feedback loop that is left totally open in the API-plus-skill model.

Without that, an agent hits a failure, gets back a generic error message, and either retries blindly or gives up. I saw that pattern enough times that it stopped feeling like bad luck and started feeling like a design flaw.

## APIs were built for humans

This is the part that took me the longest to put into words. APIs are designed with a human developer as the primary user. The choices made during API design, what to name a field, how to structure a response, where to put the edge cases in the documentation, all of those choices are optimized for a person reading them.

That is not a criticism. It is just a constraint. When you point an agent at a human-optimized API, you are asking it to operate in a space that was not designed for it. Some of that works fine. A lot of it produces quiet, persistent failures that are hard to debug and easy to dismiss as the model being dumb.

MCP was built with agents as the primary user. That changes the defaults in every small decision, and those small decisions compound.
