---
layout: page
title: About this research
permalink: /method/
---

The project studies compression of **enwik9**, a fixed, one-billion-byte extract of Wikipedia. Its goal is a complete, exactly decodable package that wins the [Hutter Prize](https://www.hutter1.net/prize/) or takes first place in the [Large Text Compression Benchmark](https://mattmahoney.net/dc/text.html). The competitions count package size differently, so they require separate final measurements.

## Why prediction is only part of the problem

A model that assigns higher probability to the next symbol can help an entropy coder store that symbol in fewer bits. But the decoder also needs the model, its weights, and every other required asset. Better predictions can produce a larger package if the extra model costs more bytes than it saves.

Our early screens measure prediction quality on selected portions of the target. We then need to check that the model survives serialization, that a real encoder and decoder agree, and that the complete package is smaller. A small test can justify the next experiment without establishing the final result.

**Bits per target** means average predictive code length for the symbols included in a particular score. Our model sees a transformed representation of the original file. A result on that representation is not directly a rate on raw Wikipedia bytes. When an essay converts a measured rate into possible whole-file savings, it names the transfer assumption; that calculation is a projection.

## Reading the journal

The essays explain a research question, the evidence that bears on it, and the resulting decision. They distinguish observations from explanations and describe what would change the conclusion. Numerical details are rounded for readability; the original reports and exact source digests remain in the research repository and in each post's source metadata. That repository is private, so the public journal is a research account rather than an independently reproducible release of every experiment.

Longer reviews are due at each five-hour milestone in cumulative charged GPU campaign time. Shorter essays cover findings that materially change the plan between milestones. Posts are written when completed work produces evidence; there is no recurring model call just to check the clock. CPU work, writing, and coordination are not included in the GPU total.

## Current accounting

| Measure | GPU-hours |
| --- | ---: |
| Cumulative charged campaign time | {{ site.data.meter.campaign_hours | round: 3 }} |
| Inherited historical total | {{ site.data.meter.inherited_anchor_hours | round: 3 }} |
| Itemized work since that total | {{ site.data.meter.itemized_hours_since_anchor | round: 3 }} |
| Next five-hour review | {{ site.data.meter.next_five_hour_boundary }} |
| Campaign ceiling | {{ site.data.meter.campaign_ceiling_hours }} |

Last accounting update: {{ site.data.meter.as_of_utc | date: "%B %-d, %Y at %H:%M UTC" }}.

The earlier material supports a retrospective of the major findings, but the available ledger does not support dividing the first 80.217 hours into honest five-hour intervals. Those hours remain visible as one historical total. The next milestone review is due at 85 hours.

The site uses the unmodified [Minima](https://github.com/jekyll/minima) theme for Jekyll. The [public source](https://github.com/jerecoder/entropy-forge-field-notes) contains the essays and site configuration.
