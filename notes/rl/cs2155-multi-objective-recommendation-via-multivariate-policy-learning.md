---
id: cs2155
title: Multi-Objective Recommendation via Multivariate Policy Learning
company: ShareChat
primary_category: rl
sub_category: bandits
year: 2024
source_url: https://arxiv.org/abs/2405.02141
tags: [multi-objective, off-policy-learning, short-video, recommendation, bandit]
---

# Multi-Objective Recommendation via Multivariate Policy Learning
**ShareChat** · 2024 · [source](https://arxiv.org/abs/2405.02141)

## Problem
Real-world recommenders juggle competing objectives — behavioral signals like clicks, shares, and dwell time plus platform goals like diversity and fairness — typically by scalarizing them into a weighted average. Choosing those weights well is the unsolved part: hand-set global weights are hard to justify and hard to keep optimal.

## Approach / System design
ShareChat treats the scalarization weights themselves as actions in a decision-making problem: a policy chooses a weight vector to maximize a North Star reward such as user retention. Since weight vectors live in a continuous multivariate action space, they extend off-policy learning methods to that domain and optimize a pessimistic lower bound on the North Star reward for safe improvement from logged data.

## Key decisions
- Optimize a North Star metric via the weights rather than tuning per-objective weights directly.
- Replace standard normal-approximation lower bounds with a policy-dependent correction, improving the coverage of the pessimistic bound.
- Deliberately design stochastic data-collection policies and sensitive reward signals so the logged data supports off-policy learning.
- Validate through the full chain: simulation, offline experiments, and online deployment.

## Stack
Off-policy bandit/policy learning extended to continuous multivariate actions with conservative (pessimistic) reward estimation. Per the catalog summary, online experiments ran on two short-video platforms each exceeding 160M monthly users. Published as a full paper at RecSys '24.

## Results
Empirical results across simulations, offline experiments, and online tests supported the approach's efficacy; the abstract reports no specific metric deltas.

## Takeaways
Framing multi-objective balancing as "learn the weights as actions against a North Star" replaces committee-tuned scalarization with a principled, data-driven policy. Pessimistic off-policy learning — with a corrected lower bound — is what makes learning such continuous policies from logs safe enough to deploy.
