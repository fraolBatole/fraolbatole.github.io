---
layout: page
title: IRepair
description: A targeted repair method that localizes and edits faulty LLM behavior while limiting disruption to general model performance.
img: assets/img/projects/irepair.svg
venue: ESEC/FSE 2025
importance: 2
category: Reliable & Verifiable AI
github: # TODO: add public repo / demo URL
related_publications: true
---

<div class="proj-meta">
  <span class="proj-chip">Co-author</span>
  <span class="proj-chip">ESEC/FSE 2025</span>
  <span class="proj-chip">Model repair</span>
</div>

<p class="proj-lead">IRepair treats harmful LLM behavior as a repair problem rather than a full retraining problem. The method localizes error-concentrated model components and applies a targeted update so the faulty behavior is reduced while unrelated capabilities are preserved.</p>

<div class="star">
  <div class="star-item">
    <span class="star-label">Problem</span>
    <p>LLMs can acquire undesired behaviors from training data, while broad fine-tuning can introduce regressions in capabilities that should remain stable.</p>
  </div>
  <div class="star-item">
    <span class="star-label">Approach</span>
    <p>IRepair localizes the model components most responsible for the faulty behavior and applies a targeted update guided by the intended output distribution.</p>
  </div>
  <div class="star-item">
    <span class="star-label">Results</span>
    <p>Across three GPT-family models from 800M to 1.6B parameters, IRepair+KL reduced toxicity by 88.7% with an 11% perplexity increase. Compared with DPO, IRepair was 43.6% more effective at repair and caused 46% less disruption.</p>
  </div>
  <div class="star-item">
    <span class="star-label">Why it matters</span>
    <p>Targeted repair supports incremental maintenance of deployed models, where localized behavior changes are preferable to repeated full-model adaptation.</p>
  </div>
</div>

See the paper for the method and evaluation {% cite imtiaz2025irepair %}.
