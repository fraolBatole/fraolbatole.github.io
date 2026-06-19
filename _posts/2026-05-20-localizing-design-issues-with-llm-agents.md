---
layout: post
title: Localizing design issues with LLM agents
date: 2026-05-20 09:00:00-0400
description: Why pinpointing where a design problem lives is harder than detecting that one exists — and how agents that combine program analysis with reasoning can help.
tags: llm-agents software-engineering
categories: research-notes
related_posts: false
---

<!-- DRAFT: starter post — review and edit before publishing. -->

Most tooling for code quality is good at _detection_ — it tells you a smell or a
design problem exists. The harder, more useful question is **localization**: _where_
in the code does the problem actually live, and what should I change?

Design issues make this especially tricky. Unlike a null-pointer bug, a poor design
decision is diffuse: it's spread across several files, it depends on intent, and the
"right" answer often requires understanding _why_ the code is shaped the way it is.
That context is exactly what classical static analysis throws away.

## Grounding reasoning in program facts

The approach I've been working on treats this as a job for an **agent** that can do
two things at once:

1. **Look at concrete program facts** — structure, dependencies, call relationships —
   the way a static analysis would.
2. **Reason in natural language** over those facts, the way a senior engineer reads a
   diff and says "this responsibility doesn't belong here."

Neither half is enough alone. Pure analysis can't weigh intent; a pure LLM hallucinates
about code it can't actually inspect. Putting the analysis _in the loop_ keeps the
agent honest, and lets it narrow a vague "something's off in this module" down to the
specific locations a developer should look at first.

## Why localization is the unlock

Localization is the bottleneck for everything downstream. If an agent can reliably say
_where_ the problem is, then automated refactoring, design repair, and review
assistance all become tractable — they finally have a target to act on.

This is the idea behind LocalizeAgent; the full method and evaluation are in the paper
on my [publications]({{ '/publications/' | relative_url }}) page. I'll use future posts
to dig into specific design decisions — how much analysis context to feed the agent, and
how to keep its conclusions verifiable.
