---
id: cs2148
title: Universal User Modeling (UUM): Foundation Model for Cross-Surface User Understanding at Snap
company: Snap
primary_category: rec
sub_category: embeddings
year: 2025
source_url: https://eng.snap.com/universal_user_modeling
tags: [foundation-model, user-embeddings, cross-surface, personalization, SIGIR, engagement-lift]
---

# Universal User Modeling (UUM): Foundation Model for Cross-Surface User Understanding at Snap
**Snap** · 2025 · [source](https://eng.snap.com/universal_user_modeling)

## Problem
Each Snapchat surface (Discover, Spotlight, etc.) modeled its users independently, optimizing surface-local metrics. This fragmented view ignored cross-surface signals, capping both understanding of broader behavior patterns and personalization quality platform-wide.

## Approach / System design
UUM is a foundation model producing shareable long-term user embeddings from over a year of behavior history, complementing each surface's short-term models. Engagement events from all major surfaces are consolidated into a unified pipeline. Each domain gets a dedicated sequence encoder (transformer / multi-head attention); encoders are connected through information bottleneck tokens that control inter-domain information flow and mitigate negative transfer, with late-stage feature fusion. Training is multi-task next-k event prediction across core surfaces. Embeddings are delivered to ranking pipelines via a real-time feature store.

## Key decisions
- Data pipeline on Spark with Iceberg storage at daily granularity, supporting flexible sampling and merging across domains.
- Event sequencing that keeps all high-intent events (boost, send) but uniformly samples low-intent events (watch), so power users' year-long sequences stay tractable.
- Per-domain encoders with bottleneck tokens instead of one monolithic cross-domain encoder, explicitly to control negative transfer.
- Cross-entropy loss for binary tasks, MSE for regression tasks.

## Stack
Spark + Iceberg data pipeline, transformer/multi-head-attention sequence encoders, information bottleneck tokens, multi-task next-k prediction, real-time feature store integration with ranking systems. Presented at SIGIR 2025.

## Results
The post reports significant engagement and DAU growth across six major use cases: Friend Stories, Ads, Spotlight, Notification, Lens, and Content Search (per-use-case metrics not disclosed in the article). Per the catalog summary, it delivered a 2.78% Story Open Rate lift.

## Takeaways
- Cross-domain signals meaningfully improve user understanding beyond any isolated surface model.
- Long-horizon behavior (1+ year) is a richer personalization foundation than short-term session features alone.
- Controlled fusion (bottleneck tokens between per-domain encoders) beats naive cross-domain pooling by limiting negative transfer.
