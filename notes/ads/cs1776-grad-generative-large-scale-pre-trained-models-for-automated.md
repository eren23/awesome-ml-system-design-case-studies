---
id: cs1776
title: GRAD: Generative Large-Scale Pre-trained Models for Automated Ad Bidding Optimization
company: Meituan
primary_category: ads
sub_category: bidding
year: 2025
source_url: https://arxiv.org/abs/2508.02002
tags: [auto-bidding, foundation-model, mixture-of-experts, causal-transformer]
---

# GRAD: Generative Large-Scale Pre-trained Models for Automated Ad Bidding Optimization
**Meituan** · 2025 · [source](https://arxiv.org/abs/2508.02002)

## Problem
Auto-bidding systems must balance overall platform performance with diverse advertiser goals and hard real-world constraints such as CPM caps and ROI targets. Traditional MDP-based approaches suffer from distribution shift between offline training and the online environment, and they explore only a limited slice of the action space, which limits how well they can serve heterogeneous advertiser preferences.

## Approach / System design
GRAD is a generative, foundation-model approach to bidding. Conditional generative models (transformers and diffusers) generate bidding trajectories tailored to advertiser preferences rather than solving a step-by-step MDP. Two components carry the design: an Action-Mixture-of-Experts module that widens exploration over diverse bidding actions, and a Value Estimator built on a Causal Transformer that performs constraint-aware optimization, keeping generated bids compliant with CPM and ROI requirements. Reward-driven generation ties the trajectories to platform and advertiser outcomes and mitigates offline-to-online distribution shift.

## Key decisions
- Frame bidding as conditional trajectory generation instead of an MDP policy, sidestepping the compounding issues of step-wise RL under distribution shift.
- Use a mixture-of-experts over actions to explore a broader, more diverse action space than a single policy would.
- Separate value estimation into a causal-transformer module so constraints (CPM, ROI) are enforced through the value side rather than post-hoc filtering.

## Stack
Conditional generative modeling with transformer and diffusion components; Action-MoE for exploration; Causal Transformer value estimator; deployed across multiple marketing scenarios at Meituan.

## Results
In production at Meituan, GRAD delivered a 2.18% increase in GMV and a 10.68% increase in ROI, validated across multiple marketing scenarios.

## Takeaways
Generative trajectory models give auto-bidding two things MDP methods struggled with: breadth of exploration (via action MoE) and native handling of advertiser-specific conditioning. Keeping constraint satisfaction inside a dedicated value estimator is what made the generative freedom safe enough for production spend.
