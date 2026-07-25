---
id: cs2088
title: "Beyond Self-Consistency: Loss-Balanced Perturbation-Based Regularization Improves Industrial-Scale Ads Ranking"
company: Meta
primary_category: ads
sub_category: ctr-prediction
year: 2025
source_url: https://arxiv.org/abs/2502.18478
tags: [regularization, perturbation, loss-balancing, deep-learning, ads-ranking, production-scale]
---

# Beyond Self-Consistency: Loss-Balanced Perturbation-Based Regularization Improves Industrial-Scale Ads Ranking
**Meta** · 2025 · [source](https://arxiv.org/abs/2502.18478)

## Problem
Industrial ads ranking models fight sparse labels and robustness issues. Self-consistency regularization (SCR) — enforcing consistent predictions under input perturbations — helps in principle, but its effectiveness is uneven across the heterogeneous settings of a production system: different surfaces, geographic regions, and client/signal-availability configurations.

## Approach / System design
The team proposes Loss-Balanced Small Perturbation Regularization (LSPR): apply small, controlled perturbations to inputs while preserving contextual integrity, enforce prediction consistency through an auxiliary loss, and — the key addition over SCR — balance the loss contributions across different data groups so no segment's distribution dominates the regularization signal. The technique is architecture-agnostic and was applied to Meta's billion-scale ads delivery ranking system.

## Key decisions
- Keep perturbations small and context-preserving rather than aggressive augmentation.
- Balance the auxiliary consistency loss across heterogeneous data groups (surfaces, regions, signal setups) instead of using a single global weight.
- Design for compatibility with any deep learning ranking architecture so it can roll out across models.

## Stack
Deep learning ranking models in Meta's ads delivery system; the method is a training-time regularization scheme, not a serving change. Specific model architectures and frameworks are not covered in the source.

## Results
LSPR consistently outperformed SCR across various groups and signal-availability setups, and was successfully deployed in a billion-scale industrial ranking system — reported as the first successful production application of perturbation-based regularization at this scale. Specific metric values are not covered in the source abstract.

## Takeaways
Regularization techniques that work in papers often fail in production because production data is a mixture of very different distributions; explicitly balancing the regularization loss across those groups is what made perturbation-based consistency viable at industrial ads scale.
