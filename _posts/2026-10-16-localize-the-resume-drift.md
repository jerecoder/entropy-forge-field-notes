---
layout: post
title: A checkpoint can restore the state and still change the experiment
summary: Two branches began from identical saved state and agreed on predictions, yet their gradients diverged. Locating the first difference changed which repair was worth testing.
research_span: QAT mechanics
campaign_range: 80.234827 → 80.270194 GPU-hours
cost_label: 127.320 GPU-seconds
outcome: Restart criterion failed
outcome_class: incomplete
evidence:
  - label: Context mechanics result
    path: reports/studies/research-coordination-20261015/released-qat-context-mechanics-result.json
    sha256: 00b7edb41d27ba2eabd00435c1bd0df33ff2f8058176055f7cac6e423133fa01
  - label: Restart localization result
    path: reports/studies/research-coordination-20261015/released-qat-restart-localization-result.json
    sha256: 31fcc3f5304fb6d1b09400efdbe8e3a7ffe1154e2b28681850f8da419c07cca1
---

Two training branches loaded the same saved checkpoint and produced identical predictions. They then took what should have been the same next update—and ended with different model states. Saving the state had worked. Reproducing the computation was a separate problem.

<!--more-->

## Why restart behavior matters for research

Long experiments are interrupted. If resuming a checkpoint changes the trajectory unpredictably, it becomes harder to interpret whether a later difference came from the experimental intervention or from execution. For a compressor, there is a second concern: the final model must also survive saving and reloading with its measured behavior intact.

The fixture was deliberately small. We retained the checkpoint after the first update, restored it into two branches, and compared the next update stage by stage. Both branches started with identical model, optimizer, random-number, and progress state.

The forward predictions and carried state matched across all four chunks. The first observed difference appeared in the accumulated gradients, before clipping or the optimizer changed the weights. That excluded the measured restoration and forward boundaries as the first source of this mismatch.

## Averages hid much of the disagreement

After the update, the branches' average code lengths differed by only about **0.00034 bits per target**. But the average *absolute* difference in individual target code lengths was about **0.0502 bits**. Changes in opposite directions largely canceled in the pooled average.

That distinction matters. A reassuring aggregate could hide substantial per-symbol numerical disagreement. Neither quantity was a compression gain: both compared two attempts at the same update on a tiny fixture.

The observed attention implementation used a memory-efficient backward operator. Because the first difference was in gradients, that operator became a concrete candidate explanation. The observation alone did not prove it was the cause; other components of the backward computation remained possible.

## One intervention was more useful than a broad sweep

The next test would replace that attention training path with the mathematical implementation while preserving the input, saved starting state, optimizer, and evaluation method. If the discrepancy disappeared, the intervention would support the original attention path as a contributor. If it remained, changing more settings at once would obscure the next diagnosis.

The localization itself cost about **11 GPU-seconds**, after the preceding context check cost about **116 seconds**. Neither answered whether the model could compress better. They made the next engineering test specific enough to be informative.

The research lesson is not that every experiment needs bitwise equality everywhere. It is that a restart failure should be localized before we decide it is harmless—or spend a larger run trying to work around it.

*The [next essay]({% post_url 2026-10-16-math-backward-control %}) reports the single intervention and the limited claim it supports.*
