---
id: cs1770
title: "LFM4Ads: A Large Foundation Model for Ads Recommendation"
company: Tencent
primary_category: ads
sub_category: ctr-prediction
year: 2025
source_url: https://arxiv.org/abs/2508.14948
tags: [foundation-model, transfer-learning, ads-recommendation, representation]
---

# LFM4Ads: A Large Foundation Model for Ads Recommendation
**Tencent** · 2025 · [source](https://arxiv.org/abs/2508.14948)

## Problem
Ads recommendation systems fail to fully exploit pre-trained foundation models: prior approaches transfer only user representations into downstream rankers, ignoring item representations and user-item cross representations, and leave a gap between how the upstream foundation model is trained and how downstream tasks consume it.

## Approach / System design
LFM4Ads is an "All-Representation Multi-Granularity" transfer framework. It comprehensively transfers three representation families from a pre-trained foundation model — user representations (URs), item representations (IRs), and user-item cross representations (CRs) — after identifying the optimal layers to extract from and aggregating CRs into transferable forms. Transfer happens at three granularities: feature-level via non-linear adapters, module-level via an Isomorphic Interaction Module that integrates cross representations, and model-level via a standalone retrieval mechanism.

## Key decisions
- Transfer all representation types (user, item, cross) rather than user embeddings alone.
- Use multiple transfer granularities (feature, module, model) to maximize how much of the foundation model's knowledge downstream tasks can absorb.
- Engineer for industrial scale from the start: terabyte-scale parameters and billions of sparse embedding keys.

## Stack
Not covered in the source beyond the model architecture itself; the system runs on Tencent's production ads platform with terabyte-scale parameters, billions of sparse embedding keys across roughly 2,000 features, processing tens of billions of samples daily.

## Results
In production since Q4 2024 with 10+ successful launches across advertising scenarios including Weixin (WeChat) Moments and Channels. Overall platform GMV lift of 2.45%, which the authors translate to estimated annual revenue increases in the hundreds of millions of dollars.

## Takeaways
The payoff from ads foundation models comes from transferring everything they learn — item and cross representations included — not just user vectors, and from matching the transfer mechanism (adapter, interaction module, retrieval) to the granularity of the downstream consumer.
