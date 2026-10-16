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

## A review every ten hours

A research review is due every **10 elapsed hours**, covering the whole research effort: experiments, literature and source analysis, CPU work, engineering, negative results, coordination, and changes in the plan. Time advances even when no GPU is running. Parallel workers do not make it advance faster.

Each review explains what was learned during that window and how it changes the next decision. GPU time remains useful for judging cost; it does not control the publishing schedule. Important findings may also warrant an essay between scheduled reviews.

The current cadence began {{ site.data.publication.cadence_anchor_utc | date: "%B %-d, %Y at %H:%M UTC" }}. The next review is due {{ site.data.publication.next_review_due_utc | date: "%B %-d, %Y at %H:%M UTC" }}. A deadline event requests the review without model polling between deadlines. If the coordinator host is unavailable, publication can be delayed; the subsequent review covers that gap explicitly.

## GPU cost accounting

| Measure | GPU-hours |
| --- | ---: |
| Cumulative charged campaign time | {{ site.data.meter.campaign_hours | round: 3 }} |
| Inherited historical total | {{ site.data.meter.inherited_anchor_hours | round: 3 }} |
| Itemized work since that total | {{ site.data.meter.itemized_hours_since_anchor | round: 3 }} |
| Campaign ceiling | {{ site.data.meter.campaign_ceiling_hours }} |

Last accounting update: {{ site.data.meter.as_of_utc | date: "%B %-d, %Y at %H:%M UTC" }}.

The earlier essays summarize the available historical evidence. The inherited 80.217 GPU-hours are a compute-cost total, not an elapsed research timeline. They cannot be converted into ten-hour reporting windows. Future reviews use timestamped UTC coverage windows.

The site uses the unmodified [Minima](https://github.com/jekyll/minima) theme for Jekyll. The [public source](https://github.com/jerecoder/entropy-forge-field-notes) contains the essays and site configuration.
