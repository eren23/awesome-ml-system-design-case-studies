---
id: cs2249
title: "TTGL: Large-scale Multi-scenario Universal Graph Learning at TikTok"
company: ByteDance
primary_category: graph
sub_category: gnn
year: 2025
source_url: https://dl.acm.org/doi/abs/10.1145/3711896.3737269
tags: [heterogeneous-graph, multi-scenario, large-scale, recommendation, user-embedding, TikTok, KDD-2025]
---

# TTGL: Large-scale Multi-scenario Universal Graph Learning at TikTok
**ByteDance** · 2025 · [source](https://dl.acm.org/doi/abs/10.1145/3711896.3737269)

## Problem
TikTok's user behavior spans many scenarios — video, search, live streaming, and e-commerce — each generating massive interaction data. TikTok needed a single framework that could handle this scale and produce unified embeddings capturing user interests across all scenarios simultaneously, rather than per-scenario silos.

## Approach / System design
TTGL (TikTok Graph Learning) builds a heterogeneous graph, TTGraph, that unifies user behaviors across scenarios and dynamically learns shared embeddings capturing the complex cross-scenario patterns. The underlying graph handles over 100 billion edges and 10 billion nodes daily. The framework couples domain-adaptive graph sampling with unsupervised training methods, and online serving pipelines deliver the embeddings for real-time recommendation while balancing efficiency and revenue.

## Key decisions
- Unify all scenarios in one heterogeneous graph rather than training scenario-specific models.
- Domain-adaptive sampling plus unsupervised training to learn fair, shared representations across scenarios of very different volumes.
- Purpose-built online serving pipelines so the universal embeddings are usable in production recommendation contexts.

## Stack
Heterogeneous GNN framework (TTGL) over the TTGraph behavior graph; domain-adaptive graph sampling; unsupervised training; online serving pipelines for real-time recommendation. Published at KDD 2025.

## Results
Offline evaluations and online A/B tests showed gains across business contexts: +0.35% 7-day retention, +3.27% watch-live duration, +1.32% gross merchandise value, +1.07% paid order count, and +1.0% search page views, spanning Feed recommendation, e-commerce, and live streaming.

## Takeaways
A single universal graph-learning system over unified cross-scenario behavior can move core business metrics in several product surfaces at once, but it requires graph infrastructure at the 100B-edges-per-day scale and sampling/training methods that handle scenario imbalance.
