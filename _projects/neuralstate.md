---
layout: page
title: NeuralState
description: A typestate analysis for statically detecting deep-learning API misuses before model training or execution.
img: assets/img/projects/neuralstate.svg
venue: IEEE TSE 2026
importance: 1
category: Reliable & Verifiable AI
github: # TODO: add public repo / demo URL
first_author: true
related_publications: true
---

<div class="proj-meta">
  <span class="proj-chip proj-chip--accent">First author</span>
  <span class="proj-chip">IEEE TSE 2026</span>
  <span class="proj-chip">Journal-first at FSE 2026</span>
  <span class="proj-chip">Typestate analysis</span>
</div>

<p class="proj-lead">NeuralState applies typestate analysis to deep-learning programs. It models valid API-state transitions for framework objects and statically reports programs that drive those objects into illegal states before a training run begins.</p>

<div class="star star--wide">
  <div class="star-item">
    <span class="star-label">Problem</span>
    <p>Deep-learning APIs often require calls to occur in a valid sequence, not merely with valid argument types. Violations can escape conventional type checking and appear only during expensive runtime execution.</p>
  </div>
  <div class="star-item">
    <span class="star-label">Approach</span>
    <p>NeuralState specifies valid state transitions for framework API objects and statically checks whether a program induces an invalid transition. The analysis reports both the offending call and the violated transition.</p>
  </div>
  <div class="star-item">
    <span class="star-label">Results</span>
    <p>On NLBench, NeuralState achieved 100% precision and 74% recall. On ExternalBench, it achieved 100% precision and 67.5% recall, with relative recall gains of 19.4% and 107% over NeuraLint.</p>
  </div>
  <div class="star-item">
    <span class="star-label">Why it matters</span>
    <p>The result shows that typestate analysis can provide static guarantees for deep-learning code, a setting where many API errors otherwise remain latent until runtime.</p>
  </div>
</div>

Read the full journal paper {% cite batole2026neuralstate %}.
