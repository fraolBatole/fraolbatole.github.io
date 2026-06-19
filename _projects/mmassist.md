---
layout: page
title: MMAssist
description: An IntelliJ IDEA assistant that recommends Move Method refactorings and delegates behavior-preserving edits to the IDE engine.
img: assets/img/projects/mmassist.svg
venue: ICSME 2025
importance: 3
category: Trustworthy AI Agents for Code
github: # TODO: add public repo / demo URL
website: https://cuboulder-se-research.github.io/move-method-assist/
related_publications: true
---

<div class="proj-meta">
  <span class="proj-chip">Co-author</span>
  <span class="proj-chip">ICSME 2025</span>
  <span class="proj-chip">Refactoring</span>
</div>

<p class="proj-lead">MMAssist studies Move Method recommendation as a combined retrieval, reasoning, and refactoring problem. It ranks candidate target classes, uses an LLM to reason over the strongest candidates, and applies the selected transformation through IntelliJ IDEA's refactoring engine.</p>

<div class="star">
  <div class="star-item">
    <span class="star-label">Problem</span>
    <p>Move Method refactoring requires identifying a target class whose responsibilities better match the method. This decision is difficult to make manually at scale and unreliable when an LLM is used without structured candidate evidence.</p>
  </div>
  <div class="star-item">
    <span class="star-label">Approach</span>
    <p>MMAssist ranks candidate target classes by semantic affinity, asks an LLM to reason over the top candidates, and applies the accepted move through the IDE refactoring engine rather than generated source edits.</p>
  </div>
  <div class="star-item">
    <span class="star-label">Results</span>
    <p>On the synthetic corpus, Recall@1 and Recall@3 reached 73% and 80%. On 210 verified real-world Move Method refactorings, Recall@1 and Recall@3 reached 71% and 82%; in a 30-participant study, 290 of 350 classes received a positive recommendation.</p>
  </div>
  <div class="star-item">
    <span class="star-label">Why it matters</span>
    <p>Separating recommendation from transformation lets the model assist the developer while the IDE supplies the behavior-preserving edit mechanism.</p>
  </div>
</div>

Project site: <a href="https://cuboulder-se-research.github.io/move-method-assist/">cuboulder-se-research.github.io/move-method-assist</a>.

Details and evaluation are in the paper {% cite icsme2025mmpro %}.
