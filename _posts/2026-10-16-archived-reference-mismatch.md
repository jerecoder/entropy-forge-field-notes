---
layout: post
title: The current scorer agreed with itself, not with the archived number
summary: A tiny released-model control showed bitwise agreement within the current runtime, while the older archived scalar check still missed its strict tolerance.
research_span: QAT mechanics
campaign_range: 80.216691 → 80.234828 GPU-hours
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
---

The first attempt ended before the model ran because an older service still owned the lane. The preserved receipt charged only **0.067 seconds**. After repairing that service boundary, the next mechanics run compared the current scorer with the archived scalar result on the same small fixture.

The current source and control agreed within the present runtime, but the archived reference still missed the registered **0.00001-bit-per-target** tolerance. Per-piece differences were about 0.0030 and 0.0053 bits per target. Their cause remained unknown, so the result did not justify a fitting claim or a relaxed criterion.

The useful conclusion was narrow: the current path could be tested further, while the historical compatibility failure stayed open and intact.
