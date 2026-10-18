---
layout: post
title: A resumable run is not yet a better compressor
summary: Full-file training survived a host change and a connection failure, but the evidence still stops short of a representative quality result. The key question is whether broad coverage can repay model storage.
research_span: Full-file teacher continuation and native exact-recovery planning, 16–18 October 2026
campaign_range: 80.698522 / 120 historical GPU-hours; separate 160-hour full-file allocation
cost_label: 3,107-second native preparation; 216.86-second GPU diagnostic; no accepted quality result
outcome: Operational recovery improved; compression advantage unmeasured
outcome_class: incomplete
evidence:
  - label: Frozen full-file design and decision rule
    path: docs/experiments/2026-10-17-full-enwik9-teacher.md
    sha256: 1f1b9698593b2bd641282e5922a08d8757b28d006c7a8fbbaaf35246c733a7af
  - label: RTX 4090 subset diagnostic
    path: reports/studies/full-enwik9-20261017/udesa-4090-trial-v1.json
    sha256: aabe9bc5f00bd6ab098786ce721a1be22bb9875291feb69d159700c5aca38972
  - label: Recovery-controller receipt
    path: reports/studies/full-enwik9-20261017/udesa-recovery-20261018.json
    sha256: bb1958fbd898693d4bd80f2c4e951ce6bfcba006720a2a9fa269e65ed82f4e16
  - label: Native preparation and baseline receipt
    path: reports/studies/full-enwik9-20261017/setup-result.json
    sha256: b72eaf931fb6021f2d0edc55883f352dc7448c361a592a489e1747cf6f1758b9
  - label: Native pair runner completion
    path: reports/studies/research-coordination-20261016-lanes/native-pair-completion-v1.json
    sha256: f45b6030bbfa7e6ed8a1ea5180d4ddcac42787f2058425379c1499e43e52a1f9
  - label: Native pair cleanup safety review
    path: reports/studies/research-coordination-20261016-lanes/native-pair-safety-fix-v1.json
    sha256: f513d17198ba0401f6b2fb367acb026e935a67bf1035a317341a45cba800db9f
  - label: FT8 baseline and cost review
    path: reports/studies/research-coordination-20261016-lanes/local-ft8-native-format-proposal-review-v1.json
    sha256: afe51f328652cfc932b5fea564ef055fafa3a1f476becda95368240eb52165b0
---

The full-file teacher has become easier to resume safely. It has not yet become a better compressor. Those are different claims, and confusing them would turn a successful recovery into a quality result we have not measured.

The important question is whether complete exposure to the transformed Wikipedia stream can improve the existing large predictor enough to pay for its stored weights. A lower prediction loss is useful evidence, but a Hutter result requires a complete exactly decodable package. The model, its coding overhead and the archive all count. The research plan therefore needs both a representative quality gate and a measured storage break-even point.

<!--more-->

## The starting model has a coverage problem to solve

The new continuation trains a 49.6-million-parameter hybrid over all 586.5 million bytes of the transformed enwik9 stream for at most five passes. Its fixed monitoring panel samples sixteen source regions, about 4.35 million scored next-symbol targets. A “bit per target” is the model's average coding cost for each predicted symbol; lower is better, but this panel score is not the size of a completed archive.

Before fitting, the released predictor scored **1.272 bits per target** on that panel and the initial teacher scored **2.021**. The teacher began **0.750 bits per target worse**, across all sixteen regions. This is a serious weakness in the starting point, not a verdict on the continuation: the panel is intentionally reused during fitting, and no post-pass comparison exists yet.

The proposed screening threshold is an improvement of **0.02 bits per target** against the released predictor. Across the full transformed target count, that would correspond to roughly **1.47 MB** of conditional payload savings. It is only a screening calculation. If the packed model adds more bytes than the payload saves, it loses the storage comparison. The panel also cannot establish training-seed uncertainty, and the chosen recipe changes both coverage and learning rate, so any gain would not isolate which change caused it.

## A useful diagnostic answered a narrower question

The laptop reached step 55,215 and 35.2 million targets—about six percent of the first full-file pass—then paused when available memory crossed its registered floor. A separate RTX 4090 check restored that checkpoint into a disposable subset run. Across 64 optimizer updates and 522,692 unique targets, its fixed subset score moved from **2.430 to 2.259 bits per target**.

That movement shows the training code can update the model on the new GPU. It does not show improvement on the sixteen-region panel: the subset is smaller, overlaps fitting, and is a different population. The measured post-warmup rate, about **12,841 targets per second**, was nearly twice an earlier laptop observation, but the workloads were unmatched. The resulting 12.7-hour-per-pass estimate excludes the 240 GB of prior data staging, larger-population overhead, full-panel scoring and interruptions. It is a scheduling hint, not a verified full-pass cost.

There was also substantial work before GPU fitting. Native PPM preparation on the Mac processed the full 586,459,020-byte source in **3,107 seconds** (about 52 minutes). Its receipt records about **216.8 GB of newly required prior chunks**, alongside **27.5 GB of reusable prior data**, and exact parity for the first 8 MiB against fresh native output. That preparation makes full-file training possible; it is a separate CPU-and-storage cost that the throughput projection does not include, and it says nothing about compression quality.

Recovery mechanics did improve. An intentional process exit resumed from the same registration without replaying the first committed group. Later, a connection loss produced a clean checkpoint; two external copies were hash-verified and a CPU reload checked optimizer state, random state and the exact cursor before the recovery controller resumed the frozen job. These checks make partial work safer to preserve. They do not establish current live status or model quality, and this review does not infer either from an older “running” snapshot.

The full-file allocation is **160 active worker hours**, including a reserved two-hour terminal scoring phase and an existing calendar stop. It is distinct from the historical campaign, whose **80.699 of 120 GPU hours** remain its own cost record. The subset diagnostic's conservative charge was 216.86 seconds against the new allocation. No budget or historical ledger was reset. No new external literature finding changed the plan during this review.

## Native exact recovery is now a testable engineering path

The separate FT8 route asks whether a compact model can survive a real native encode/decode pair. Its baseline review found that the older timing receipt used a different weights hash from the current file, so that timing is not a matched comparison. A conservative planning estimate left only about 42 seconds below a six-minute cap. That makes a single aggregate deadline and a safe shutdown path part of the experiment's design, not housekeeping.

The pair runner now puts baseline and candidate round trips under one reservation, checks each arm's pinned inputs and exact recovered bytes, and stops before the candidate if the baseline fails. A safety review also fixed bounded process-group cleanup so an uncertain worker leaves the reservation open instead of pretending the charge is complete. Focused software checks passed. A read-only Mac review verified the available pins, ledger and resource snapshot, but no codec was built or run and no experiment registration was created. This is execution readiness, not scientific acceptance.

Coordination itself consumed noticeable resources. One read-only Mac review used **105,353 input tokens**—80,640 cached and 24,713 uncached—and 6,549 output tokens; its receipt omitted a required memory field, leading to one follow-up check. The local proposal review did not report token usage, so the total is unknown. Future boundary reports should carry the exact admission fields and token split, and should summarize only changes since the previous receipt.

## What would change the plan

The next decision should come from the first complete full-file pass, not from another subset speed test. Compare the same fixed panel against both baselines, report region coverage, and inspect the learning curve before spending the remaining passes in the existing allocation. Partial exposure remains incomplete evidence. At the declared endpoint, score the actual serialized and reloaded INT7 model, then compare saved payload bytes with model and decoder bytes. A likelihood gain alone is not a compression win; no sixth pass follows automatically.

The native FT8 pair remains a separate, small test of exact recovery. It should run only under a finite registration that preserves the current ledger and proves aggregate timeout, cleanup and resource admission. Its success would establish that a particular artifact decodes exactly. It would not establish representative quality or a Hutter/LTCB win.

The latest reviewed records demonstrate better recovery and stronger experiment plumbing. They leave the main scientific uncertainty intact: whether complete coverage produces enough packed-model improvement to repay its storage cost. Until that comparison and exact package recovery exist, the honest result is progress in measurement readiness, with no accepted compressor candidate.
