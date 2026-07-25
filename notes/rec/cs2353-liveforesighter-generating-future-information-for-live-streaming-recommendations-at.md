---
id: cs2353
title: "LiveForesighter: Generating Future Information for Live-Streaming Recommendations at Kuaishou"
company: Kuaishou
primary_category: rec
sub_category: ranking
year: 2025
source_url: https://arxiv.org/abs/2502.06557
tags: [live-streaming, future-prediction, generative-model, ranking, real-time, sequential-modeling]
---

# LiveForesighter: Generating Future Information for Live-Streaming Recommendations at Kuaishou
**Kuaishou** · 2025 · [source](https://arxiv.org/abs/2502.06557)

## Problem
Live-streaming recommendation differs fundamentally from static short-video recommendation: the content of a stream changes continuously over time, and the most valuable user behaviors (sending digital gifts, buying products) typically require long watch sessions of more than ten minutes. The system must therefore identify streams that match a user's current interests while also predicting which streams will still satisfy them in the near future — before enough interaction data on the current stream state exists.

## Approach / System design
Kuaishou proposes LiveForesighter, a framework that generates future information about live streams to support real-time ranking decisions. Instead of relying only on historical interaction signals, the system forecasts how a stream's content and appeal will evolve, injecting these generated future signals into the recommendation model so it can rank streams by expected future satisfaction rather than past behavior alone.

## Key decisions
- Treat the dynamic, ever-changing nature of live content as a first-class modeling problem rather than reusing static-content recommenders.
- Generate predictive/future contextual signals for streams to compensate for the lag between content changes and accumulated user feedback.
- Target long-horizon engagement (long watch sessions that precede gifting and purchases) rather than immediate click signals.

## Stack
Not covered in the source.

## Results
Not covered in the source (the paper is marked as work in progress; detailed offline/online results were not available in the fetched content).

## Takeaways
For live content, historical interaction data is structurally stale: by the time feedback accumulates, the stream has changed. Generating forward-looking information about content is a way to close that gap and make ranking decisions aligned with where a stream is going, not where it has been.
