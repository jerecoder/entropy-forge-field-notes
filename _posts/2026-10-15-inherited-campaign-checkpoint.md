---
layout: post
title: Why a smaller model can be the better compressor
summary: After roughly eighty GPU-hours, the clearest lesson was that prediction quality, model storage, and target coverage have to be evaluated together.
research_span: Historical retrospective
campaign_range: 80.216691 GPU-hours inherited
cost_label: Earlier per-run allocation unavailable
outcome: No candidate selected
outcome_class: open
evidence:
  - label: Candidate decision
    path: reports/studies/research-coordination-20261015/candidate-decision.json
    sha256: 69ce29558038cc359345e7b81cce7c2c364ef0b8ceffe610f58e638c3f9cd608
  - label: Frontier mechanism decision
    path: reports/studies/research-coordination-20261015/frontier-decision.json
    sha256: c04939a6509a7e32ee64299d97f98a024587aa34aab56271ab454e961ce26b25
---

A model can learn to predict a piece of Wikipedia remarkably well and still make a poor compressor. After roughly eighty GPU-hours of research, that was the most consequential finding: our strongest local prediction result had not earned its storage cost, and its performance did not carry over to the rest of the file.

<!--more-->

## The model has to pay for itself

In ordinary machine learning, the trained model is often treated as infrastructure. In compression, it is part of the message. The decoder needs the weights before it can recover the text, so those weights count against any savings from better predictions.

One of our models used about **44.4 MB of weights**. On the eight-mebibyte region it had been fitted to, it achieved about **0.502 bits per target**, compared with **1.061** for the released compact model. That looks like a substantial improvement. The compact model, however, needed only about **2.93 MB of weights**.

Even under the favorable assumption that the fitted-region improvement carried across the entire transformed file, the larger model would increase the combined weights-and-predictions subtotal by about **0.51 MB**. That calculation excludes other codec components; it is not a measured archive size. It is enough to show why a strong local loss number did not justify promoting the model.

Reducing its precision cut the weight cost, but also damaged the predictions. In the corresponding six-bit version, the same conditional subtotal grew by about **1.87 MB**. The smaller file of weights produced a worse projected subtotal.

## The more serious problem was coverage

That favorable extrapolation was also unsupported. The available broader fitting endpoints remained behind the released model. One distributed fitting run finished at **1.665**, against a matched released baseline of **1.272**, on roughly 4.35 million targets drawn from sixteen regions.

These are different populations from the fitted eight-mebibyte region. The numbers cannot be placed in one league table. The useful comparison is each model against its matched baseline on the same symbols.

Together, the results point to two distinct obstacles. The large model had to recover a substantial storage cost, and the local fitting success did not establish useful quality across the target. A further precision adjustment could address the first obstacle only if it preserved enough quality; it could not, by itself, establish the missing coverage.

This does not prove that the architecture lacks capacity or that more training would fail. The available runs do not establish convergence. It does mean that another small recipe variation needs a reason to change the candidate decision.

## What this changed about the plan

The next investment should test a mechanism with a credible route to a smaller complete package. That could mean improving the already compact released model, or finding a causal correction whose added state and code cost little. It should begin with a cheap comparison that can reject the idea before a long training or native implementation effort.

The final standard remains demanding: serialize the model, measure it again, recover the exact bytes with a real decoder, and count every required artifact. A prediction improvement buys the next test; it does not finish that chain.

The historical ledger records **80.217 GPU-hours**, but does not support reconstructing exact five-hour intervals. This essay summarizes the decision supported by the available evidence rather than assigning invented boundaries to those hours.

*The [next essay]({% post_url 2026-10-16-archived-reference-mismatch %}) examines an earlier question in that chain: how to tell whether a change in a score came from the model or the measurement.*
