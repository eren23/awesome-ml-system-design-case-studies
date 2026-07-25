---
id: cs2298
title: "GAS: Generative Auto-bidding with Post-training Search"
company: Kuaishou
primary_category: rl
sub_category: sequential-decision
year: 2024
source_url: https://arxiv.org/abs/2412.17018
tags: [auto-bidding, generative-model, advertising, post-training, multi-constraint-bidding]
---

# GAS: Generative Auto-bidding with Post-training Search
**Kuaishou** · 2024 · [source](https://arxiv.org/abs/2412.17018)

## Problem
Generative (decision-transformer-style) auto-bidding models condition on targets like return-to-go, but in sequential bidding those conditions become misaligned with the actual value of the actions taken. The models also inherit the majority preferences of their training data, so they generalize poorly to minority advertiser preferences — and retraining a separate model per preference is prohibitively expensive.

## Approach / System design
GAS keeps a single base generative bidding policy and refines its outputs at decision time with a post-training search strategy. Small critic models are trained for different advertiser preferences, and an MCTS-inspired search uses them to align the base model's actions with the desired preference — a "weak-to-strong" alignment where lightweight critics steer a stronger generative model. A voting mechanism over transformer-based critics (trained with policy indications) selects refined actions. For high-frequency preference scenarios where search overhead matters, GAS also provides fine-tuning methods as a computationally efficient alternative.

## Key decisions
- Refine at inference with search instead of retraining the base model per preference, avoiding the cost of maintaining many models.
- Use small per-preference critics plus MCTS-style search for weak-to-strong alignment of the generative policy.
- Aggregate critic opinions through a voting mechanism rather than trusting a single critic.
- Reserve fine-tuning for high-frequency preferences where amortizing training cost beats paying search cost per decision.

## Stack
Transformer-based generative bidding policy, small transformer critic networks, MCTS-inspired search with critic voting. Deployed on Kuaishou's advertising platform. Further infrastructure details are not covered in the source.

## Results
- 4.60% improvement in target cost, validated on a real-world dataset and in online A/B tests on the Kuaishou ad platform.

## Takeaways
Post-training search is a practical middle path for production generative bidding: one base model plus cheap critics and search adapts to heterogeneous advertiser preferences without retraining, and the compute trade-off (search at inference vs. fine-tuning) can be chosen per preference frequency.
