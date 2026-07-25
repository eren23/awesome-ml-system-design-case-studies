---
id: cs1768
title: RankMixer: Scaling Up Ranking Models in Industrial Recommenders
company: ByteDance
primary_category: ads
sub_category: ctr-prediction
year: 2025
source_url: https://arxiv.org/abs/2507.15551
tags: [ranking, scaling, token-mixing, moe, serving-efficiency]
---

# RankMixer: Scaling Up Ranking Models in Industrial Recommenders
**ByteDance** · 2025 · [source](https://arxiv.org/abs/2507.15551)

## Problem
Industrial ranking models sit under strict latency and QPS constraints for both training and serving, and their feature-crossing modules were designed in the CPU era — they fail to exploit modern GPUs, leaving Model Flops Utilization (MFU) at only 4.5%. That hardware inefficiency, plus the quadratic cost of self-attention, made it impractical to scale ranking model capacity the way LLMs have scaled.

## Approach / System design
RankMixer is a hardware-aware ranking architecture. It keeps the parallelism of transformers but replaces quadratic self-attention with multi-head token mixing, which is far cheaper on GPUs. Per-token FFNs preserve distinct modeling of separate feature subspaces and their cross-feature interactions, instead of collapsing everything into shared parameters. To push toward a billion parameters, a Sparse-MoE variant expands capacity, with a dynamic routing strategy that counters inadequate training and imbalance across experts. The design targets trillion-scale production datasets.

## Key decisions
- Replace handcrafted, low-MFU feature-crossing modules with a unified architecture designed around GPU hardware characteristics.
- Swap self-attention for multi-head token mixing to eliminate the quadratic cost while retaining transformer-style parallelism.
- Use Per-token FFNs so each feature subspace keeps dedicated modeling capacity.
- Scale via Sparse-MoE with dynamic routing to keep experts balanced and well-trained.

## Stack
GPU-oriented dense and Sparse-MoE ranking architecture (multi-head token mixing + Per-token FFNs), trained on trillion-scale production data and served across ByteDance's recommendation and advertising scenarios.

## Results
MFU improved from 4.5% to 45%, and model parameters scaled roughly 100x while keeping inference latency about the same. The 1B dense-parameter RankMixer was launched to full traffic without increased serving cost. Online A/B tests showed a 0.3% increase in user active days and a 1.08% increase in total in-app usage duration.

## Takeaways
Scaling laws can be brought to ranking models if the architecture is co-designed with the hardware: a 10x MFU improvement is what made a 100x parameter increase affordable at constant latency. The bottleneck for industrial recommenders was not data or ideas but arithmetic efficiency of legacy feature-interaction modules.
