---
id: cs1786
title: DRL-PUT: Deep Reinforcement Learning for Ranking Utility Tuning in the Ad Recommender System at Pinterest
company: Pinterest
primary_category: ads
sub_category: ctr-prediction
year: 2025
source_url: https://arxiv.org/abs/2509.05292
tags: [reinforcement-learning, ranking-utility, hyperparameter-tuning, multi-objective, deep-rl, utility-tuning, ads-ranking, personalization]
---

# DRL-PUT: Deep Reinforcement Learning for Ranking Utility Tuning in the Ad Recommender System at Pinterest
**Pinterest** · 2025 · [source](https://arxiv.org/abs/2509.05292)

## Problem
Pinterest's ad ranking scores candidates with a utility function that linearly combines predictions for multiple business objectives. The combination weights were tuned manually, which is suboptimal on several fronts: the tuning objective itself is unprincipled, the space of parameter combinations is far too large to search by hand, and a single global setting cannot personalize to users or adapt to seasonality.

## Approach / System design
DRL-PUT reframes utility-weight selection as a reinforcement learning problem: given the context of an ad request, a policy model predicts the hyperparameter values that maximize a predefined reward. A deliberate design choice is to skip value-function estimation entirely — the reward distribution in this setting is high-variance and imbalanced, making value estimation unreliable — and instead learn the policy directly from online serving logs. The learned policy emits per-request utility weights, so the ranking utility adapts dynamically per user and context rather than being a static global configuration.

## Key decisions
- Replace manual global weight tuning with a per-request learned policy, adding personalization and seasonal adaptability.
- Learn the policy directly from production serving logs rather than estimating a value function, to sidestep high-variance, imbalanced rewards.
- Define the reward carefully as the optimization target; ablations examined how reward definition shapes outcomes.

## Stack
Deep RL policy model trained on Pinterest's online serving logs, integrated into the production ad recommender's ranking utility stage. Specific architectures and infrastructure are not covered in the source.

## Results
In online A/B experiments on Pinterest's production ad system, DRL-PUT improved CTR by 9.7% and long-click-through rate by 7.7% over the manually tuned baseline. Ablation studies analyzed reward definitions and the personalization behavior of the policy.

## Takeaways
The scoring formula's mixing weights — often the least principled part of a mature ranking system — are themselves a high-leverage ML surface. Making them a per-request policy output turned static heuristics into personalized, adaptive control, and the direct policy-learning shortcut (no value function) is a practical pattern wherever rewards are noisy and skewed.
