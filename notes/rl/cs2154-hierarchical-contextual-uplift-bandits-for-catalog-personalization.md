---
id: cs2154
title: Hierarchical Contextual Uplift Bandits for Catalog Personalization
company: Dream11
primary_category: rl
sub_category: bandits
year: 2025
source_url: https://arxiv.org/abs/2601.14333
tags: [contextual-bandits, uplift-modeling, catalog-personalization, fantasy-sports, cold-start]
---

# Hierarchical Contextual Uplift Bandits for Catalog Personalization
**Dream11** · 2025 · [source](https://arxiv.org/abs/2601.14333)

## Problem
Contextual bandits degrade in highly dynamic environments like fantasy sports, where user behavior and reward distributions shift rapidly with match schedules and events. Frequent retraining is expensive, and new users/contexts face cold-start with no policy to lean on.

## Approach / System design
Dream11 built a hierarchical contextual uplift bandit framework for catalog personalization. The hierarchy lets the system dynamically adjust contextual granularity, falling back from user-specific contexts to broader system-wide levels when data is thin, and sharpening to individual users when it is rich. Contextual similarity across levels enables policy transfer, which mitigates cold-start, and uplift modeling principles focus the policy on incremental impact rather than raw response rates.

## Key decisions
- Multi-level context hierarchy spanning system-wide insights down to per-user contexts, rather than a single fixed granularity.
- Policy transfer via contextual similarity to handle cold-start and volatile reward regimes without constant full retraining.
- Integrate uplift modeling into the bandit objective so actions are chosen for their incremental effect.

## Stack
Contextual bandit algorithms with hierarchical context management and uplift modeling on Dream11's fantasy sports platform; specific algorithms and infrastructure are not detailed in the abstract.

## Results
A/B tests on Dream11 showed a 0.4% revenue improvement alongside better user-satisfaction metrics. After full rollout as the default system in May 2025 — per the catalog summary, serving 160M+ users — it delivered an additional 0.5% revenue improvement.

## Takeaways
When reward distributions churn quickly, adaptivity in the context structure itself (not just the arm values) is what keeps a bandit useful: hierarchies plus similarity-based transfer buy robustness to drift and cold-start. Small relative revenue gains compound meaningfully at hundreds of millions of users.
