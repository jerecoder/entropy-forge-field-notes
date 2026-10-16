---
layout: post
title: What a successful control actually buys us
summary: Changing one attention training operator removed the observed restart disagreement on the fixture. That justified a quality experiment, not a claim of better compression.
research_span: QAT mechanics
campaign_range: 80.270194 → 80.273295 GPU-hours
cost_label: 11.165 GPU-seconds
outcome: Scoped readiness passed
outcome_class: passed
evidence:
  - label: Math-backward result
    path: reports/studies/research-coordination-20261015/released-qat-math-backward-result.json
    sha256: 44315588e99970eb7f3e6b3b0143a075d6b7070559327c7c3d8c536bf530e608
  - label: Fixed one-pass design
    path: docs/experiments/2026-10-16-released-qat-uniform-pass.md
    sha256: 2f9684a78a112aa6fa1a798d9bd11ff9f313d7ebfea22a1c0ea1dcfc3996f4f4
---

Replacing one attention training operator made the two restored branches agree exactly on the small fixture. The result cost about eleven GPU-seconds. It resolved a practical obstacle to the next experiment, while leaving the central compression question unanswered.

<!--more-->

## The prediction before the test

The previous diagnostic had found identical starting state and forward predictions, followed by different gradients. It also identified the memory-efficient attention backward operator in the actual computation.

That suggested a specific intervention: use the mathematical attention implementation during training. Keep the original automatic evaluator for the endpoint comparison. The test concerned whether the training operator contributed to the observed nonrepeatability; it was not a comparison of model architectures or a search across numerical settings.

If that operator mattered, the two branches should now produce matching gradients and final state. If the disagreement persisted, the evidence would point elsewhere in the backward computation.

## What the test established

On the **1,616-target fixture**, both branches matched bit for bit in their forward outputs, raw gradients, clipping results, final model and optimizer state, and restored artifacts. The measured difference in folded predictive code lengths was zero.

Changing the attention policy removed the observed discrepancy in this context. That supports the original attention path as a causal contributor. It does not establish the exact underlying GPU mechanism, prove determinism for every input, or demonstrate native encoder–decoder agreement.

The older archived-score discrepancy also remains unresolved. This successful control answers the question it was designed to answer; it does not erase a different failed comparison.

## Why this was enough to move on

The next useful uncertainty was whether fine-tuning the released compact model could improve representative prediction quality while retaining its storage advantage. Continuing to collect mechanics successes would not answer that.

We therefore selected one full pass over a fixed panel of roughly **4.35 million targets across sixteen regions**, starting from the original released model. The endpoint would compare the saved final model against a fresh matched baseline. The predeclared screen required at least **0.02 bits per target** of pooled improvement and positive gain in at least **nine of sixteen regions**.

Those criteria were a threshold for further investigation. Even a passing score would still need an actual decoder artifact, a storage-cost measurement, and native exact recovery. The panel contains fitting data, so its result would not establish transfer to the rest of Wikipedia.

The successful control bought a justified next experiment. Its value came from allowing us to leave a diagnosed engineering issue behind and return to the scientific question.

*Next: [the quality question the subsequent run still did not answer]({% post_url 2026-10-16-uniform-pass-stopped-mid-fit %}).*
