---
layout: post
title: When a benchmark changes without the model changing
summary: An unchanged model received a different score. Before treating small improvements as progress, we had to establish which comparisons the measurement could support.
research_span: QAT mechanics
campaign_range: 80.216691 → 80.234827 GPU-hours
cost_label: 65.289 GPU-seconds
outcome: Compatibility unresolved
outcome_class: incomplete
evidence:
  - label: Mechanics result
    path: reports/studies/research-coordination-20261015/released-qat-mechanics-result.json
    sha256: d85c646a8a662c45f7ee9fbba0a865a726a4f05a7c9fec2a83c11e26fc0c22f6
  - label: Startup repair decision
    path: reports/studies/research-coordination-20261015/released-qat-mechanics-startup-repair.json
    sha256: 50411791246cdbfe49d72b85bfae104e2bc6a1b9fe3a4d033b773024009574ad
  - label: Current-runtime mechanics registration
    path: configs/experiments/ivanov-hybrid/released-qat-mechanics-20261016-v2-supervision.json
    sha256: 7aa5f0d3c2467363d09bdeb19d22484aeea0cd21654035b47f08cb6afd695c8c
  - label: Independent original-source comparison under the current runtime
    path: reports/studies/research-coordination-20261015/released-qat-context-mechanics-result.json
    sha256: 00b7edb41d27ba2eabd00435c1bd0df33ff2f8058176055f7cac6e423133fa01
---

We loaded the released model without training it and obtained a different score from the archived reference. The discrepancy was small, but large enough to fail the planned compatibility check. Before asking whether fine-tuning improved compression, we had to ask whether the measuring instrument was stable.

<!--more-->

## Why a small discrepancy matters

Our proposed fine-tuning screen looked for an improvement of at least **0.02 bits per scored target**. A change in numerical execution could contaminate that comparison: we might attribute a better score to learning when some of it came from a different evaluation path.

The initial check used just two pieces of text, containing **1,616 scored targets** in total. The current evaluation differed from the archived result by about **0.0030 and 0.0053 bits per target** on the two pieces. Both exceeded the declared compatibility tolerance of 0.00001.

These differences were below the planned useful effect, but that did not make them irrelevant. Their behavior on the larger panel was unknown, and the purpose of a control is to establish the comparison before interpreting the experimental result.

## Agreement can answer the wrong question

Two executions of the current path agreed exactly. That established repeatability within that context. It did not establish agreement with the old measurement: two copies can share the same change or defect.

A later control independently invoked the archived scoring functions under the current runtime and compared them with the current path. They agreed bit for bit on the fixture. Source and input checks also matched the original weights, model configuration, and selected text.

That substantially narrowed the problem. It supported the current implementation's agreement with the original source in the present context. It did not identify the cause of the older scalar discrepancy. The runtime environment had changed, among other possible execution differences, and the compact archived evidence did not contain a layer-by-layer trace that could resolve the cause.

## The resulting research decision

The useful path was a fresh, matched control under the current runtime: measure the unchanged released model and the trained candidate using the same evaluator and the same symbols. The historical mismatch remains a recorded failure of historical compatibility. A new comparison cannot retroactively make it pass.

This distinction lets the project advance without pretending that every uncertainty has been removed. We need enough evidence to trust the comparison being made, and an explicit account of what it does not establish.

The first two attempts charged about **65 GPU-seconds**. They produced no learned improvement and no verdict against fine-tuning. Their value was in identifying which measurement needed to be controlled before spending more on the hypothesis.

*Next: [why restoring a checkpoint was not enough to reproduce the next update]({% post_url 2026-10-16-localize-the-resume-drift %}).*
