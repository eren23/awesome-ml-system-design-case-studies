---
id: cs2165
title: "OneRank: Unified Transformer-Native Ranking Architecture for Multi-Task Recommendation"
company: Shopee
primary_category: search
sub_category: learning-to-rank
year: 2026
source_url: https://arxiv.org/abs/2606.16838
tags: [multi-task-ranking, transformer, production, e-commerce, GMV, Southeast-Asia]
---

# OneRank: Unified Transformer-Native Ranking Architecture for Multi-Task Recommendation
**Shopee** · 2026 · [source](https://arxiv.org/abs/2606.16838)

## Problem
Transformer-based recommenders typically decouple a shared feature encoder from downstream multi-task prediction heads. That split creates an information bottleneck under heterogeneous task objectives, gradient interference between tasks (the seesaw effect), and a mismatch between dynamic attention-based representation learning and static task predictors.

## Approach / System design
OneRank removes the encoder-predictor separation and performs multi-task reasoning inside the Transformer stack itself. Task-private channels give each objective (click, add-to-cart, order) specialized capacity while limiting cross-task interference. The forward pass performs task-conditioned information selection, candidate-aware contextualization, and controlled cross-task interaction; the backward pass uses cross-task gradient detachment to isolate task-specific parameter updates and prevent negative transfer. Static MLP scorers are replaced with dynamic matching-based scoring for context-aware personalized ranking, and per the catalog summary, task scores are fused to optimize GMV over up to 4,096 candidate items per request.

## Key decisions
- Internalize multi-task prediction in the Transformer rather than hanging task towers off a shared encoder.
- Give tasks private channels plus explicitly controlled interaction, instead of fully shared or fully separate parameters.
- Detach cross-task gradients in the backward pass to kill seesaw effects at the optimization level.
- Score via dynamic matching rather than static MLP heads.

## Stack
Transformer-native multi-task ranking architecture with task-private optimization paths and gradient isolation, deployed in Shopee's large-scale e-commerce ranking system.

## Results
Offline and online experiments on large-scale industrial datasets showed OneRank significantly outperforms state-of-the-art baselines while maintaining computational efficiency; the abstract does not report specific metric numbers.

## Takeaways
The standard "shared encoder + task towers" recipe leaves multi-task conflicts unresolved; integrating task reasoning into the attention stack with gradient isolation addresses interference where it originates. Architectural unification here also simplifies the path from multi-task scores to a business objective like GMV.
