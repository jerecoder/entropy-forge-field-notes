---
layout: post
title: The representative pass stopped before its terminal score
summary: A matched baseline completed, then the user stopped the fit at group 109 of 296; the saved optimizer checkpoint is preserved for a separately registered continuation.
research_span: Representative QAT screen
campaign_range: 80.273295 → 80.697843 GPU-hours
cost_label: 1,528.373 GPU-seconds
outcome: Incomplete · no quality result
outcome_class: incomplete
evidence:
  - label: Audited interruption receipt
    path: reports/studies/research-coordination-20261015/released-qat-uniform-pass-interruption.json
    sha256: 80cd05e479e94aa64058b668bef26a12022cf0e81183be4aa1bf2be6db3bea24
  - label: One-pass registration and thresholds
    path: docs/experiments/2026-10-16-released-qat-uniform-pass.md
    sha256: 2f9684a78a112aa6fa1a798d9bd11ff9f313d7ebfea22a1c0ea1dcfc3996f4f4
---

The fresh full-panel baseline completed. Training then reached **step 109 of 296**, applying 1,489,148 of 4,349,745 representative targets. The stop request arrived between optimizer groups; the last complete state was saved with its optimizer and random-number state.

The supervisor finalized the charge once at **1,528.373 seconds** and verified that the worker cgroup had closed. No terminal paired score ran. The run therefore says nothing yet about the registered 0.02-bit-per-target and 9-of-16-region screen, and it does not pass packed quality, native recovery, package size, or competition eligibility.

The next step is a new, separately pinned continuation from the saved cursor. It must preserve this stopped run, reuse the completed baseline only after exact identity checks, finish the remaining groups once, and attach its actual report and supervisor exit before scientific review.
