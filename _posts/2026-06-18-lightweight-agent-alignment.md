---
layout: post
title: Keeping coding agents aligned with the original task
date: 2026-06-18 09:00:00-0500
description: The story behind RefineAct, a formal runtime-verification approach for checking whether each agent action still matches the user's intent.
tags: coding-agents software-engineering refineact
categories: research-notes
related_posts: false
---

When I was migrating parts of the Boa infrastructure to a new server, I kept running into the same problem with coding agents. The task was narrow: configure a service, adjust a deployment setting, inspect a failing command, or make one small change. The agent understood the request at the start, but the execution drifted.

It would create files I did not ask for. It would modify files outside the scope of the task. It would hardcode table values in the database instead of fixing the configuration path that produced them. Sometimes it made changes that were not only unnecessary, but actively made the system harder to reason about.

This happened most often when I used cheaper coding-agent modes after exhausting higher-quality tokens. The agent was not useless. It could make progress, but it did not reliably preserve the original intent as it moved from one tool call to the next.

That distinction matters. A coding agent does not only answer a question. It acts on a codebase, a shell, a database, and sometimes a deployment environment. Once action is involved, being directionally helpful is not enough. The agent needs a check that asks a simpler question before each step:

> Is this proposed action still aligned with the original task?

As a quick practical experiment, I tried a lightweight MCP guardrail that asked this question before each action was executed. It was useful as a sanity check and often worked better than a bare agent, but it was only a motivating prototype. The deeper problem is formal: once an agent can act, the system needs a principled way to decide whether the next action is permitted by the original intent.

## The failure mode

The failure I saw during the Boa migration was not dramatic. It was ordinary drift.

I would ask for one change, and the agent would infer a larger repair plan. I would ask it to inspect a configuration problem, and it would edit nearby files because they looked relevant. I would ask it to preserve the current data, and it would still try to patch the symptom by changing database contents.

In isolation, each action looked defensible. In sequence, the behavior was wrong. The agent had substituted a local sense of progress for the actual user goal.

Public incidents show the same shape at higher stakes. In the [reported Replit incident](https://www.tomshardware.com/tech-industry/artificial-intelligence/ai-coding-platform-goes-rogue-during-code-freeze-and-deletes-entire-company-database-replit-ceo-apologizes-after-ai-engine-says-it-made-a-catastrophic-error-in-judgment-and-destroyed-all-production-data), an agent deleted production data despite instructions that should have prevented destructive changes. [Reports about Meta](https://www.theverge.com/ai-artificial-intelligence/897528/meta-rogue-ai-agent-security-incident) described another pattern: an internal assistant gave advice in the wrong context, contributing to a security incident, and a separate internal agent reportedly deleted emails without permission.

The common issue is not only that agents make mistakes. The issue is that an agent can take an action that violates the task boundary while still appearing to work toward the task.

## The RefineAct idea

RefineAct is the formal approach that grew out of this concern: action-level alignment should be checked before execution, not only after a task succeeds or fails.

RefineAct adds a runtime verification step between the agent's proposed action and the environment that will execute it.

The loop is simple:

1. The user gives the original task.
2. The agent proposes the next action.
3. A verifier checks whether that action is consistent with the original task and its constraints.
4. If the action is acceptable, it runs.
5. If the action violates the task boundary, it is rejected and the agent must refine the action.

The important part is where the check happens. RefineAct does not only inspect the final answer. It checks the action before it touches the system. The verifier gives the task intent an operational role: it becomes a constraint on the next action, not a sentence that only mattered at the beginning of the conversation.

That placement matters for coding agents. A bad final answer is annoying. A bad shell command, file edit, database update, or deployment change can leave damage behind. Runtime verification gives the system a chance to stop the action before it becomes state.

## Takeaway

The main takeaway from RefineAct is that intent should remain active throughout the agent's execution, not only at prompt time. A coding agent should be judged action by action against the task it was asked to perform.

This is the core shift. Prompting tries to make the agent remember the goal. RefineAct gives the system a formal mechanism for checking whether the next action still satisfies that goal. The optional MCP guardrail showed the practical value of checking actions at runtime, but RefineAct is the principled version of that idea: a runtime-verification framework for keeping agent actions within the user's intended boundary.
