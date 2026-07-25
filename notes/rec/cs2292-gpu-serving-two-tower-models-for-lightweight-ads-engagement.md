---
id: cs2292
title: GPU-Serving Two-Tower Models for Lightweight Ads Engagement Prediction
company: Pinterest
primary_category: rec
sub_category: candidate-generation
year: 2026
source_url: https://medium.com/pinterest-engineering/gpu-serving-two-tower-models-for-lightweight-ads-engagement-prediction-5a0ffb442f3b
tags: [gpu-serving, two-tower, ads, engagement-prediction, ctr, cost-per-click]
---

# GPU-Serving Two-Tower Models for Lightweight Ads Engagement Prediction
**Pinterest** · 2026 · [source](https://medium.com/pinterest-engineering/gpu-serving-two-tower-models-for-lightweight-ads-engagement-prediction-5a0ffb442f3b)

## Problem
Pinterest's lightweight ads ranking stage served two-tower engagement-prediction models entirely on CPU. That capped model sophistication: any architecture rich enough to improve prediction quality would blow the latency budget, so performance and serving cost were locked in a trade-off.

## Approach / System design
The team kept the two-tower paradigm — Pin embeddings computed offline in batch, user embeddings generated in real time — but replaced the previous Multi-Task Multi-Domain (MTMD) model with a new architecture combining Multi-gate Mixture-of-Experts (MMOE) and Deep & Cross Networks (DCN), and moved serving to GPUs so the added complexity fits within latency limits. Training was segmented by scenario, with standard and shopping ads trained on only their relevant data.

## Key decisions
- Migrate from domain-specific modules toward a unified MMOE-based design for multi-domain handling.
- Switch to GPU serving specifically to unlock model complexity, not just to cut latency.
- Segment training by ad scenario (standard vs. shopping) rather than pooling all data.
- Invest in training-efficiency work (dataloader, fused kernels, BF16, configuration tuning) so iteration speed scaled with model complexity.

## Stack
GPU serving on p4d instances with 1TB CPU memory; MMOE + DCN architectures; BF16 precision training; fused kernels; KL-divergence loss.

## Results
Offline: 5–10% reduction in CTR-prediction loss versus the prior production model, with a further 5–10% from scenario segmentation. Online: significant cost-per-click reductions and CTR increases across all segments. Model iteration speed doubled.

## Takeaways
For lightweight ranking, the serving substrate is the real constraint on model quality — GPU migration unlocked architectural headroom that CPU serving had foreclosed. Scenario-segmented training was a cheap, effective complement, and training-efficiency investment is what made the more complex models operationally sustainable.
