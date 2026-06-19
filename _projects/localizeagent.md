---
layout: page
title: LocalizeAgent
description: An evidence-grounded agent for localizing design issues in Java programs using structured program facts and iterative reasoning.
img: assets/img/projects/localizeagent.svg
venue: ICSE 2025
importance: 2
category: Trustworthy AI Agents for Code
github: https://github.com/fraolBatole/LocalizeAgent
first_author: true
related_publications: true
---

<div class="proj-meta">
  <span class="proj-chip proj-chip--accent">First author</span>
  <span class="proj-chip">ICSE 2025</span>
  <span class="proj-chip">Program analysis + LLM</span>
</div>

<p class="proj-lead">LocalizeAgent investigates design-issue localization as an evidence-grounded reasoning task. It combines structured program facts with iterative LLM reasoning so each localization claim can be traced back to concrete code evidence.</p>

<div class="star star--wide">
  <div class="star-item">
    <span class="star-label">Problem</span>
    <p>Design issues such as misplaced responsibilities and weak cohesion are diffuse and context dependent. Without structured program evidence, LLM localizations can appear plausible while remaining weakly anchored in the code.</p>
  </div>
  <div class="star-item">
    <span class="star-label">Approach</span>
    <p>LocalizeAgent extracts dependency graphs, call graphs, responsibility profiles, and coupling signals, then uses an iterative agent loop to reason over those facts and refine the suspected fault location.</p>
  </div>
  <div class="star-item">
    <span class="star-label">Results</span>
    <p>On real-world Java refactoring data, LocalizeAgent reports relative exact-match accuracy gains of 138%, 166%, and 206% for information hiding, complexity, and modularity issues, respectively.</p>
  </div>
  <div class="star-item">
    <span class="star-label">Why it matters</span>
    <p>Evidence-grounded localization provides a stronger basis for downstream refactoring because the agent's recommendation is connected to explicit program facts.</p>
  </div>
</div>

<p class="proj-links">Code is available at <a href="https://github.com/fraolBatole/LocalizeAgent">github.com/fraolBatole/LocalizeAgent</a>.</p>

The full method, evaluation, and results are in the paper {% cite batole2025localizeAgent %}.
