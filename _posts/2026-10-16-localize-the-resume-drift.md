---
layout: post
title: A saved step was not enough to make training repeatable
summary: The model restored, but the next optimizer update diverged; a targeted comparison located the first mismatch in the attention backward pass.
research_span: QAT mechanics
campaign_range: 80.234828 → 80.270194 GPU-hours
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

The retained step-one checkpoint loaded, and its forward pass matched the uninterrupted run. The two branches then took the same second-update loss, but their raw gradients differed. A focused localization found the first split in the memory-efficient attention backward operator.

That difference mattered after saving: the two branches’ folded code-length estimates differed by **0.050156 bits per target** on the tiny fixture, far above the registered repeatability threshold. This was a restart-mechanics failure, not a quality result about the model.

The evidence pointed to one useful control: use math-only scaled dot-product attention during training, while keeping the original automatic folded evaluator. It did not justify a backend sweep or a relaxed threshold.
