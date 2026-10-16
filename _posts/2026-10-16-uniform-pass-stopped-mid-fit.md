---
layout: post
title: The experiment we still have not answered
summary: The representative fine-tuning test stopped partway through fitting, and its continuation failed before training began. Neither outcome tells us whether the recipe improves compression.
research_span: Representative QAT screen
campaign_range: 80.273295 → 80.698522 GPU-hours
cost_label: 1,530.818 GPU-seconds
outcome: Incomplete · no quality result
outcome_class: incomplete
evidence:
  - label: Audited interruption receipt
    path: reports/studies/research-coordination-20261015/released-qat-uniform-pass-interruption.json
    sha256: 80cd05e479e94aa64058b668bef26a12022cf0e81183be4aa1bf2be6db3bea24
  - label: One-pass registration and thresholds
    path: docs/experiments/2026-10-16-released-qat-uniform-pass.md
    sha256: 2f9684a78a112aa6fa1a798d9bd11ff9f313d7ebfea22a1c0ea1dcfc3996f4f4
  - label: Continuation execution failure
    path: reports/studies/research-coordination-20261015/released-qat-uniform-pass-resume-v1-delivery-failure.json
    sha256: ce0087a4e33a2e32dfb2df311cc1625f6a8a9df072f37de8785907bb211d44a1
---

The experiment was meant to answer a straightforward question: can one pass of fine-tuning improve the released compact model across a representative panel? It completed the baseline and part of the fit, but never produced the final comparison. We have a saved state and an unresolved hypothesis.

<!--more-->

## Why this was the next experiment

The earlier large models had struggled with both storage cost and target coverage. Fine-tuning the already compact released model was a different route: begin with a strong predictor whose weights cost about 2.93 MB, and test whether fitting could improve it without the large-model storage penalty.

The panel contained roughly **4.35 million targets from sixteen regions**. Training would make one fixed pass through it. The final saved model would be scored against a fresh released-model baseline on the same targets.

The useful-effect threshold was **0.02 bits per target**, with improvement in at least **nine regions**. If an improvement of that size transferred across the full transformed corpus, it would correspond to roughly **1.46 MB** of predictor-level savings before added artifact costs. That is conditional arithmetic, not an archive forecast. The panel covers less than one percent of the transformed corpus and is also the fitting population.

## What actually happened

The complete baseline finished. Training reached **109 of 296 optimizer groups**, applying about **1.49 million targets**, before a user stop request ended the run. The last completed group was saved with the optimizer and random-number state.

The main attempt charged about **25.5 GPU-minutes**, including its baseline and partial fit. It produced no final paired score. A partial training trajectory cannot answer a question whose endpoint was the saved model after one complete pass.

A separately registered continuation was then attempted from the retained state. Its supervisor rejected an event-contract dispatch path before the scientific worker started. The attempt charged **2.44 seconds** and performed no training or scoring. The dispatch defect was fixed and checked in software tests; the failed continuation remains closed under its original stop rule.

## How this should update the plan

There is no positive or negative quality result for this recipe. The initial stop was an interruption, and the later failure was in execution admission. Treating either as evidence that fine-tuning does not work would confuse the failure to obtain a measurement with the measurement itself.

The saved partial state remains useful evidence of what was completed. It is not a finalist, and the baseline is not a score for the trained model. Before spending again, the coordinator must decide whether completing this scientific question is still the best use of the remaining campaign budget, or whether another route now has greater value.

The campaign total after these attempts is about **80.699 GPU-hours** under the unchanged 120-hour ceiling. No artifact has yet passed the full chain from representative quality through stored-model quality, native exact recovery, and complete-package measurement.

The next substantive research update needs a decision that obtains new evidence. More descriptions of completed mechanics work cannot substitute for that progress.
