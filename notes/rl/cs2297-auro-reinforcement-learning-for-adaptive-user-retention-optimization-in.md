---
id: cs2297
title: "AURO: Reinforcement Learning for Adaptive User Retention Optimization in Recommender Systems"
company: Kuaishou
primary_category: rl
sub_category: policy-optimization
year: 2023
source_url: https://arxiv.org/abs/2310.03984
tags: [recommendation, user-retention, non-stationarity, short-video, state-abstraction]
---

# AURO: Reinforcement Learning for Adaptive User Retention Optimization in Recommender Systems
**Kuaishou** · 2023 · [source](https://arxiv.org/abs/2310.03984)

## Problem
Using RL to optimize long-term user retention in a recommender system runs into non-stationarity: user behavior patterns continually evolve, shifting both environment dynamics and reward distributions. A policy trained on yesterday's interaction patterns degrades as interaction rates and retention propensities drift, and novel behavior patterns create an implicit cold-start problem for the policy.

## Approach / System design
AURO adds an adaptive state abstraction module inside the policy network to make the policy robust to a changing environment. The abstraction is trained with a value-based loss aligned to current policy performance, so it reflects environment changes as they happen and drives policy adjustment. To keep exploration safe in a cost-sensitive online setting, AURO applies performance-based rejection sampling that guards recommendation quality while the policy adapts. The system was evaluated in a user-retention simulator, on MovieLens, and on a live short-video recommendation platform.

## Key decisions
- Tackle non-stationarity with a learned state abstraction rather than frequent full retraining, letting the policy adapt to drift and to cold-start-like novel behavior patterns.
- Align the abstraction's training loss with current policy value, so representation and policy stay in sync as the environment shifts.
- Use performance-based rejection sampling as guarded exploration, since unconstrained RL exploration is too costly on a production recommender.

## Stack
Policy network with an adaptive state abstraction module and a value-based auxiliary loss; user-retention simulator plus live short-video platform for evaluation. Specific infrastructure details are not covered in the source.

## Results
AURO showed superior performance against all evaluated baseline algorithms across the simulator, MovieLens, and the live short-video recommendation platform. Specific numeric lifts are not stated in the source. The work was presented at The Web Conference (WWW) 2025 as an oral.

## Takeaways
Retention-oriented RL in production must treat non-stationarity as a first-class problem: a state abstraction trained against current policy value adapts to drift without retraining, and guarded exploration is essential when every bad recommendation has a real cost.
