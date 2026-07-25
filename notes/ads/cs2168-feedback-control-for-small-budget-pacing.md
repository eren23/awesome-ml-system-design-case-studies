---
id: cs2168
title: Feedback Control for Small Budget Pacing
company: Snap
primary_category: ads
sub_category: budget-pacing
year: 2025
source_url: https://arxiv.org/abs/2509.25429
tags: [budget-pacing, feedback-control, pid-controller, real-time-bidding, small-budget]
---

# Feedback Control for Small Budget Pacing
**Snap** · 2025 · [source](https://arxiv.org/abs/2509.25429)

## Problem
Budget pacing must spread a campaign's spend to match its goals inside a dynamic auction environment. Existing pacing methods lean on ad-hoc parameter tuning, which causes instability and inefficiency — worst for small-budget campaigns, where noisy feedback makes naive controllers oscillate.

## Approach / System design
A principled controller grounded in control theory: bucketized hysteresis combined with proportional feedback to track the desired spend rate stably and adaptively. The work also provides a framework for selecting controller parameters across campaigns of varying sizes, replacing per-campaign hand-tuning, and was validated in real-world auction experiments.

## Key decisions
- Bring feedback-control theory into the pacing system instead of continuing ad-hoc heuristic tuning.
- Bucketized hysteresis to damp reaction to noisy spend signals (critical at small budgets).
- Proportional feedback for adaptive tracking of the target spend rate.
- A parameter-selection framework so the controller generalizes across heterogeneous campaigns.

## Stack
Control-theoretic pacing controller deployed against real-world auction traffic. No further infrastructure details in the source.

## Results
- 13% reduction in pacing error vs. the baseline method.
- 54% reduction in λ-volatility (spend-multiplier volatility) vs. baseline.

## Takeaways
Pacing is a control problem, and treating it as one pays off: a principled hysteresis + proportional-feedback design delivers steadier, more accurate spend than tuned heuristics, with the biggest wins for the small-budget campaigns that ad-hoc methods handle worst.
