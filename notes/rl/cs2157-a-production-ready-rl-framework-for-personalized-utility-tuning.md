---
id: cs2157
title: A Production-Ready RL Framework for Personalized Utility Tuning with Pareto Sweeping in Pinterest Recommender Systems
company: Pinterest
primary_category: rl
sub_category: policy-optimization
year: 2026
source_url: https://arxiv.org/abs/2605.16344
tags: [utility-tuning, multi-objective, pareto, homefeed, ranking]
---

# A Production-Ready RL Framework for Personalized Utility Tuning with Pareto Sweeping in Pinterest Recommender Systems
**Pinterest** · 2026 · [source](https://arxiv.org/abs/2605.16344)

## Problem
Large-scale recommenders blend multiple objectives into a single utility score, but the blending weights are tuned manually, applied globally to all users, slow to adapt as the environment and business priorities change, and hard to govern when leadership wants to shift trade-offs.

## Approach / System design
PRL-PUTS reframes utility-weight tuning as a one-step, value-based RL problem: given request-level context, an agent picks the utility-weight vector that maximizes engagement, so weights become personalized and adaptive per request. On top of this, inference-time Pareto sweeping varies scalarization parameters to generate a family of policies and an empirical Pareto frontier over objective trade-offs, which decision makers use as a governance artifact to select operating points.

## Key decisions
- One-step value-based formulation instead of a full sequential RL problem — enough to personalize weights while staying tractable and safe for production.
- Ranker-independent design that runs in parallel with ranking inference, adding negligible serving latency.
- Sweep the Pareto frontier at inference time so policy trade-offs can be changed instantly by decision makers, without retraining.
- Validate offline using unbiased exploration logs before online rollout.

## Stack
Value-based RL conditioned on request-level context; scalarization-based multi-objective sweeping and empirical Pareto frontier construction; deployment alongside the existing Homefeed ranker. Further infrastructure details are not covered in the source.

## Results
In online experiments on Pinterest Homefeed, PRL-PUTS produced a +0.13% increase in successful sessions, a core user-engagement metric, versus baseline approaches.

## Takeaways
Utility-weight tuning — usually a manual, global knob — can be personalized with a lightweight one-step RL agent without touching the ranker or the latency budget. Exposing an explicit Pareto frontier turns multi-objective trade-offs from an opaque tuning exercise into a governable business decision.
