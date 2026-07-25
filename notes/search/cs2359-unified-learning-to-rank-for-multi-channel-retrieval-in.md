---
id: cs2359
title: Unified Learning-to-Rank for Multi-Channel Retrieval in Large-Scale E-Commerce Search
company: Target
primary_category: search
sub_category: semantic-search
year: 2026
source_url: https://arxiv.org/abs/2602.23530
tags: [learning-to-rank, multi-channel-retrieval, e-commerce-search, gradient-boosting, feature-fusion]
---

# Unified Learning-to-Rank for Multi-Channel Retrieval in Large-Scale E-Commerce Search
**Target** · 2026 · [source](https://arxiv.org/abs/2602.23530)

## Problem
Large-scale e-commerce search merges candidates from multiple specialized retrieval channels (e.g., keyword, semantic, bestsellers, trending, seasonal) into one ranked list. Traditional fusion methods such as Reciprocal Rank Fusion apply fixed global weights, ignoring query-specific channel utility and inter-channel interactions — leaving conversion on the table.

## Approach / System design
Target reformulates multi-channel fusion as a query-dependent, channel-aware learning-to-rank problem over heterogeneous candidate sources. A single unified ranking model learns to merge and rank documents from all channels, jointly optimizing multiple business objectives (clicks, add-to-carts, purchases) with channel-specific objectives incorporated into the model. Recent user behavioral signals are integrated to capture short-term intent shifts relevant to conversion. The model is deployed in production on Target.com under strict latency constraints.

## Key decisions
- Replace static fusion heuristics (fixed global channel weights) with a learned, query-dependent fusion model.
- Make the ranker channel-aware so it can exploit per-query channel utility and inter-channel interactions.
- Optimize jointly for multiple funnel objectives (clicks, add-to-carts, purchases) rather than a single relevance target.
- Incorporate recent user behavior for short-term intent, tied to conversion.
- Engineer for production latency: p95 under 50 ms.

## Stack
Not covered in the fetched source beyond the unified LTR model (catalog metadata indicates a gradient-boosted ranker).

## Results
Online A/B testing on Target.com showed a +2.85% improvement in user conversion versus rank-based fusion methods, while meeting the p95 < 50 ms production latency requirement.

## Takeaways
Fusion is a ranking problem, not a plumbing problem: which retrieval channel matters depends on the query, and learning that mapping — with multi-objective, behavior-aware LTR — beats any fixed blending scheme. The gains came from smarter combination of existing channels, not from new retrieval capacity.
