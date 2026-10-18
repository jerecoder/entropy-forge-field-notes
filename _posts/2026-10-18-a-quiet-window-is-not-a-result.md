---
layout: post
title: More training is not yet better compression
summary: The full-file job recovered and continued through the deadline, reaching about one quarter of its target population. That is real execution progress, but no completed pass or new fixed-panel quality score has arrived.
research_span: 18 October 2026, 20:03–21:29 UTC (85 minutes)
campaign_range: Existing full-file authorization; no new finalized cost entry
cost_label: 35.7 minutes of additional reported process time; GPU charge not closed
outcome: Recovery and training progressed; scientific acceptance remains open
outcome_class: incomplete
evidence:
  - label: Previous review and unresolved quality comparison
    path: _posts/2026-10-18-a-resumable-run-is-not-a-better-compressor.md
    sha256: 634d8bb766b344824803a6bb832acee1e3b842039bf83dd0100cd0971eb6f706
---

The full-file teacher continued through this review’s deadline, but the evidence still does not show whether it is a better compressor. That distinction matters: a process that can recover and consume more data is useful engineering progress, while compression quality requires a comparable score and ultimately an exactly decodable package.

A recovery check passed at step 61,238, with 125.6 million targets applied. The first observation in this review window, at 20:53 UTC, showed the worker initializing; by the deadline at 21:29:17 it was training at step 62,965 with 152.1 million distinct targets applied. The fixed population contains 586.2 million scored targets, so this is about 26% of one full coverage pass. No pass had completed. The first snapshot came nearly fifty minutes after the window began, so the record does not tell us how the process spent that earlier portion.

The quality evidence did not move with the exposure count. The recorded fixed-panel history still contains only the starting score of 2.021 bits per target, while the released predictor’s comparison score is 1.272. “Bits per target” is average predicted coding cost for each scored symbol; lower is better. The last individual training batch reported 2.30 bits per target, but batches cover different regions and are not a replacement for the fixed panel. The run marks quality versus the released predictor unverified. More target exposure cannot be called a gain until a comparable panel score is recorded.

A checkpoint at step 62,812 was verified on both local storage and the Mac. That reduces the risk that a host or connection problem destroys accumulated work; it does not make the checkpoint a scientific result. The worker’s elapsed-time counter advanced by about 35.7 minutes between the first and last in-window snapshots. This is process runtime, not a finalized GPU charge, and no new closed cost entry appeared in the reviewable record. No new literature analysis or CPU study result was recorded either.

At the deadline, the latest observation said “training,” and the changed records contained no supervisor-exit report. The execution state is therefore still active in the observed evidence, not complete. The next useful boundary is a completed full-coverage pass with the fixed-panel score by region, followed by the registered packed-model and exact-recovery checks. Until then, the correct conclusion is narrower: recovery worked, coverage increased to roughly one quarter, and scientific acceptance did not change. No figure is included because the new measurements track exposure, not model quality.
