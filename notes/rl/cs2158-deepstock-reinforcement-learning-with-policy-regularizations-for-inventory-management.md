---
id: cs2158
title: "DeepStock: Reinforcement Learning with Policy Regularizations for Inventory Management"
company: Alibaba
primary_category: rl
sub_category: policy-optimization
year: 2025
source_url: https://arxiv.org/abs/2603.19621
tags: [inventory-management, policy-regularization, tmall, deep-rl, supply-chain]
---

# DeepStock: Reinforcement Learning with Policy Regularizations for Inventory Management
**Alibaba** · 2025 · [source](https://arxiv.org/abs/2603.19621)

## Problem
Deep RL looks attractive for inventory replenishment, but in practice it is highly sensitive to hyperparameters and performs inconsistently in the real world, which has kept it from being trusted for large-scale supply-chain decisions.

## Approach / System design
DeepStock injects classical inventory theory — notably Base Stock policy structure — into deep RL as policy regularizations. Instead of letting the policy network learn replenishment behavior from scratch, the learned policy is constrained toward the shapes that decades of operations research say are near-optimal, while the RL component adapts to real demand dynamics. The approach is evaluated across multiple DRL algorithms rather than tuned for one, and validated in both synthetic experiments and production deployment on Tmall.

## Key decisions
- Encode domain knowledge (Base Stock concepts) as regularization on the policy rather than as a hard-coded rule or a separate baseline policy.
- Compare across several DRL methods to show the regularization effect is general, reframing "which DRL algorithm is best" for inventory management.
- Prove out in production at full scale, not just simulation.

## Stack
Deep reinforcement learning with inventory-theory-derived policy regularizations, deployed on Alibaba's Tmall e-commerce platform; specific algorithms and infrastructure are not detailed in the abstract.

## Results
Reached 100% deployment of regularized DRL on Tmall — per the catalog summary, covering replenishment for over 1 million SKU-warehouse pairs as of October 2025. Policy regularizations significantly accelerated hyperparameter tuning and improved final policy performance versus unregularized DRL.

## Takeaways
Grounding a learned policy in classical theory is a practical cure for DRL's brittleness: the regularizer narrows the search space, so tuning is faster and outcomes are more reliable. The gains came from theory-informed constraints more than from algorithm choice, a useful pattern for any domain with strong classical baselines.
