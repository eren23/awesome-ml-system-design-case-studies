---
id: cs1785
title: Exploration in Online Advertising Systems with Deep Uncertainty-Aware Learning
company: Alibaba
primary_category: ads
sub_category: ctr-prediction
year: 2021
source_url: https://arxiv.org/abs/2012.02298
tags: [exploration, uncertainty, gaussian-process, ad-ranking]
---

# Exploration in Online Advertising Systems with Deep Uncertainty-Aware Learning
**Alibaba** · 2021 · [source](https://arxiv.org/abs/2012.02298)

## Problem
Production CTR prediction models are strong at exploitation but have no principled exploration mechanism: they keep serving ads the model is already confident about. Classical contextual bandit methods provide exploration but are hard to marry with the deep neural networks that power modern personalization, because they lack the flexibility of DNN function approximators.

## Approach / System design
Alibaba proposes Deep Uncertainty-Aware Learning (DUAL): CTR models built on Gaussian processes that retain the representational flexibility of deep networks while producing predictive uncertainty estimates alongside point predictions. Those uncertainty estimates plug into established bandit-style exploration strategies, so the ad ranking layer can trade off exploiting high-CTR ads against exploring ads whose CTR is uncertain. DUAL-based ranking policies are then deployed on top of existing production models.

## Key decisions
- Use Gaussian processes layered on deep networks to get calibrated uncertainty without giving up DNN flexibility.
- Connect the uncertainty estimates to well-studied bandit algorithms rather than inventing a bespoke exploration heuristic.
- Design for easy deployment on existing production models with minimal computational overhead, since ad serving is latency-sensitive.

## Stack
GP-based uncertainty estimation on top of deep neural CTR models; bandit-algorithm-derived exploration/ranking strategies integrated into Alibaba's display advertising system.

## Results
On several public datasets the method's effectiveness was validated offline. In an online A/B test on Alibaba's display advertising platform, the DUAL-based ranking policy delivered an 8.2% lift in social welfare and an 8.0% lift in revenue.

## Takeaways
Uncertainty-aware deep models close the exploration gap that pure-exploitation CTR systems leave open, and the exploration payoff shows up directly in business metrics. Grounding exploration in uncertainty estimates lets a production system reuse the mature bandit literature instead of ad-hoc randomization.
