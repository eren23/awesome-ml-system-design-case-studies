---
id: cs1772
title: TokenMixer-Large: Scaling Up Large Ranking Models in Industrial Recommenders
company: ByteDance
primary_category: ads
sub_category: ctr-prediction
year: 2026
source_url: https://arxiv.org/abs/2602.06563
tags: [ranking, scaling, sparse-moe, token-mixing, mixture-of-experts, rankmixer]
---

# TokenMixer-Large: Scaling Up Large Ranking Models in Industrial Recommenders
**ByteDance** · 2026 · [source](https://arxiv.org/abs/2602.06563)

## Problem
Large ranking architectures such as Wukong, HiFormer, and DHEN struggle with sub-optimal designs and hardware under-utilization, capping their practical scalability. ByteDance's own earlier TokenMixer/RankMixer generation hit its own ceilings: vanishing gradients in deeper configurations, incomplete sparsification, and constrained depth — all obstacles to pushing ranking models into the multi-billion-parameter regime.

## Approach / System design
TokenMixer-Large evolves the RankMixer line with three main changes. Mixing-and-reverting operations with inter-layer residuals stabilize gradient flow through deep stacks. Auxiliary loss mechanisms further support deeper configurations. And a Sparse Per-token Mixture-of-Experts replaces dense expansion, expanding parameters efficiently so capacity grows without proportional compute. Together these let the model scale to 7B parameters in production and 15B in offline experiments.

## Key decisions
- Fix gradient propagation first (mixing-and-reverting with inter-layer residuals plus auxiliary losses) — depth was the blocker before size.
- Choose sparse per-token MoE over dense expansion for parameter scaling, completing the sparsification the earlier architecture left partial.
- Evolve the deployed architecture incrementally rather than replacing it, keeping production continuity across ByteDance scenarios.

## Stack
Sparse Per-token MoE token-mixing architecture, an evolution of RankMixer, deployed across ByteDance's e-commerce, advertising, and live streaming ranking systems.

## Results
Scaled to 7B parameters in production (15B offline). Reported online gains: e-commerce +1.66% orders and +2.98% per-capita preview payment GMV; advertising +2.0% ADSS; live streaming +1.4% revenue.

## Takeaways
Getting ranking models from ~1B to 7–15B parameters was less about a new idea and more about systematically removing the previous generation's bottlenecks — gradient stability for depth, full sparsification for width. Incremental architecture evolution, validated per business line, delivered measurable revenue impact across three distinct scenarios.
