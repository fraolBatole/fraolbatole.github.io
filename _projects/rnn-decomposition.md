---
layout: page
title: RNN Decomposition
description: A modularization technique for decomposing trained RNNs into reusable and replaceable behavioral components.
img: assets/img/projects/rnn-decomposition.svg
venue: ICSE 2023
importance: 3
category: Reliable & Verifiable AI
github: # TODO: add public repo / demo URL
related_publications: true
---

<div class="proj-meta">
  <span class="proj-chip">Co-author</span>
  <span class="proj-chip">ICSE 2023</span>
  <span class="proj-chip">Modularity</span>
</div>

<p class="proj-lead">This project studies whether trained recurrent neural networks can be decomposed into modules after training. The goal is to make learned behavior reusable and replaceable without retraining the entire model from scratch.</p>

<div class="star">
  <div class="star-item">
    <span class="star-label">Problem</span>
    <p>Trained RNNs are typically treated as monolithic artifacts, so reusing or replacing a learned behavior often requires retraining the full network.</p>
  </div>
  <div class="star-item">
    <span class="star-label">Approach</span>
    <p>The method identifies module boundaries inside a trained RNN and decomposes the model into units that capture distinct learned behaviors for reuse or replacement.</p>
  </div>
  <div class="star-item">
    <span class="star-label">Results</span>
    <p>The evaluation used 5 canonical datasets and 4 model variants per dataset. Decomposition changed accuracy by -0.6% and BLEU by +0.10%; reuse changed accuracy by -2.38% and BLEU by +4.40%; replacement changed accuracy by -7.16% and BLEU by +0.98%.</p>
  </div>
  <div class="star-item">
    <span class="star-label">Why it matters</span>
    <p>Post-training modularity gives neural systems a maintainability path closer to software systems, where localized components can be reused or replaced independently.</p>
  </div>
</div>

Full approach and results are in the paper {% cite imtiaz2023decomposing %}.
