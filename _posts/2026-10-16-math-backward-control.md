---
layout: post
title: One attention change restored fixture-level repeatability
summary: Math-only attention made the two resumed updates bitwise agree on the registered fixture, which supported one representative pass but did not pass a model-quality gate.
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

The training-only intervention replaced the observed memory-efficient attention backward path with math-only scaled dot-product attention. Both branches then matched bitwise across their starts, updates, optimizer state, saved checkpoints, and folded reloads. The original automatic evaluator stayed unchanged.

This passed a **fixture-local continuation check**. The older archived-reference scalar check and default-runtime restart criterion stayed failed, and no candidate-quality or package gate changed. The result supported one bounded experiment: start from the released step-zero model, fit one complete source-order pass, then score the persisted final checkpoint against a fresh matched baseline.
