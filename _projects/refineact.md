---
layout: page
title: RefineAct
description: A runtime verification framework for checking an LLM agent's proposed actions before execution.
img: assets/img/projects/refineact.svg
venue: ASE 2026
importance: 1
category: Trustworthy AI Agents for Code
github: https://github.com/fraolBatole/aligned
first_author: true
related_publications: true
---

<div class="proj-meta">
  <span class="proj-chip proj-chip--accent">First author</span>
  <span class="proj-chip">ASE 2026</span>
  <span class="proj-chip">Runtime verification</span>
</div>

<p class="proj-lead">RefineAct studies LLM-agent reliability at the boundary between proposed action and executed action. It inserts a runtime verification layer that checks whether a candidate action is consistent with the task intent before the action is allowed to affect the environment.</p>

<div class="star star--wide">
  <div class="star-item">
    <span class="star-label">Problem</span>
    <p>Standard agent frameworks can execute a tool action as soon as the model produces it. If the action is unsafe or inconsistent with the task, the error may become visible only after the environment has already changed.</p>
  </div>
  <div class="star-item">
    <span class="star-label">Approach</span>
    <p>RefineAct inserts a verification layer between action generation and execution. Candidate actions are checked against a task-intent specification, and rejected actions are regenerated before they can run.</p>
  </div>
  <div class="star-item">
    <span class="star-label">Results</span>
    <p>The work is reported in an ASE 2026 paper, and the public lightweight implementation is linked as <code>aligned</code> while the full paper artifact is prepared for release.</p>
  </div>
  <div class="star-item">
    <span class="star-label">Why it matters</span>
    <p>Checking actions at runtime provides an auditable control point for agent behavior, complementing prompt design and model training with an execution-time reliability mechanism.</p>
  </div>
</div>

<p class="proj-links"><a href="https://github.com/fraolBatole/aligned">aligned</a>, a lightweight, non-formal implementation, is available now. The full code from the paper will be released shortly.</p>

The formal approach and complete evaluation are in the paper {% cite batole2026refineact %}.
