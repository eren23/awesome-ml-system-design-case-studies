---
id: cs2261
title: "Beyond Winning: Spotify's Experiments with Learning Framework"
company: Spotify
primary_category: mlops
sub_category: experimentation
year: 2025
source_url: https://engineering.atspotify.com/2025/9/spotifys-experiments-with-learning-framework
tags: [experimentation, a/b-testing, metrics, confidence-platform, learning-rate, experiment-quality, product-development]
---

# Beyond Winning: Spotify's Experiments with Learning Framework
**Spotify** · 2025 · [source](https://engineering.atspotify.com/2025/9/spotifys-experiments-with-learning-framework)

## Problem
As Spotify's Confidence experimentation platform scaled to hundreds of teams, win rate became a misleading success measure. In a mature product, experiments that catch regressions or produce well-powered neutral results are as valuable as wins — they prevent bad ships and kill invalid ideas — but a win-rate lens counts them as failures, distorting how experimentation value is perceived and incentivized.

## Approach / System design
The Experiments with Learning (EwL) framework classifies each experiment as learning or non-learning based on two gates:
- **Validity**: proper implementation — no failed health checks, correct traffic routing.
- **Decision-readiness**: the result supports a decision, in one of three forms: a success (ship an improvement with no regressions), a detected regression (abort and iterate), or a neutral-but-powered result (enough data that an effect would have been detected if present).

The learning rate — the share of experiments producing decision-ready insight — becomes the headline platform metric instead of win rate.

## Key decisions
- Require all relevant metrics to be adequately powered (not just one) before a result counts as decision-ready.
- Count experiment restarts separately, surfacing implementation problems rather than hiding them.
- Scope the metric to product R&D experiments, excluding ad-campaign evaluations.
- Add anti-gamification guardrails: keep monitoring win rate, experiment volume, and precision alongside learning rate.

## Stack
Confidence (Spotify's internal A/B testing platform), its SDKs and instrumentation, sample-size calculators, health-check monitoring, and multi-metric analysis tooling.

## Results
- Learning rate of roughly 64%, versus a win rate around 12% in experiment-heavy organizations — a 52-point gap capturing the value of regression detection and powered neutral results.
- Platform adoption grew from ~40 to ~300 teams by end of 2022; over 58 teams ran 520 experiments on the mobile home screen in a year.

## Takeaways
For mature products, experimentation's main value shifts from finding wins to preventing regressions and eliminating invalid ideas — the success metric should reflect that. Redefining the metric changes culture (encouraging iteration and honest reporting), but needs guardrails so a softer target doesn't get gamed.
