---
layout: page
title: Compositional Generalization in Mathematical Reasoning
description: Why LSTMs and Transformers fail to generalize on arithmetic, and the data bug that invalidated the first round of results
img: /assets/img/generalization_gap.png
importance: 2
category: Research
github: https://github.com/bcode0127-debug/Compositional-Reasoning-Arithmetic.git
related_publications: false
---

Neural networks fail at compositional generalization in ways that are not obvious from training metrics: a model can look strong in-distribution while never having learned the underlying algorithm. This study tests that failure systematically on arithmetic expression evaluation, with strict out-of-distribution splits for length and for tree depth.

## The result that mattered most was catching my own mistake

An early version of this project produced clean, publishable-looking OOD numbers. Before trusting them, I audited the pipeline and found an input-truncation bug that had corrupted 99% of the OOD evaluation set. Every prior result was invalid. I rebuilt the datasets to decouple expression length from tree depth using controlled tree-shape generation, then re-ran everything as a 12-run seed matrix (2 architectures, 2 studies, 3 seeds) so the corrected findings were stable rather than one lucky run.

## Corrected findings

- The **LSTM** reaches 35.7% held-out accuracy, with graded length decay from 14.8% down to 2.1% across 4 to 7 operations. It degrades, but gracefully.
- A **2.6x-larger Transformer** memorizes training data to 98% yet generalizes at only 7.3%, stable across all seeds. More capacity bought memorization, not reasoning.
- Behaviorally, 63% of LSTM errors land within 2x of the true magnitude versus 25% for the Transformer, and the Transformer fails at the very first decoding step 71% of the time, evidence that it learned answer format without performing the underlying computation.

## Why it matters

The gap between looking correct and being correct is central to trusting a model. A system that produces the right-looking output without computing it is exactly the failure mode interpretability and evaluation need to surface. This project is an argument for treating interpretability as an empirical discipline with the same rigor as production ML: falsifiable hypotheses, controlled experiments, and evaluation sets you have actually validated.

## Ongoing work

Attention-circuit analysis of the corrected models, to test whether the Transformer's first-step failure corresponds to a specific breakdown in attention routing. Findings are being compiled into a research paper targeting arXiv.
