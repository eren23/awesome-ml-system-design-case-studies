---
id: cs2169
title: Multi-Faceted Large Embedding Tables for Pinterest Ads Ranking
company: Pinterest
primary_category: ads
sub_category: ctr-prediction
year: 2025
source_url: https://arxiv.org/abs/2508.05700
tags: [embedding-tables, ads-ranking, ctr-prediction, large-scale, feature-engineering]
---

# Multi-Faceted Large Embedding Tables for Pinterest Ads Ranking
**Pinterest** · 2025 · [source](https://arxiv.org/abs/2508.05700)

## Problem
Pinterest wanted large embedding tables in its ads ranking models, but hit two walls: the usual sparsity/scalability issues, and — more surprisingly — training large embedding tables from scratch produced neutral metrics, so raw capacity alone bought nothing. GPU memory limits also constrained serving.

## Approach / System design
Two-part solution:
1. **Multi-faceted pretraining** — enrich embedding-table representations by combining multiple pretraining algorithms rather than a single method, then use these pretrained embeddings in CTR and CVR ranking models.
2. **CPU-GPU hybrid serving** — a serving architecture that splits work across CPU and GPU to get around GPU memory constraints while keeping latency flat.

## Key decisions
- Pretrain embeddings with several complementary algorithms instead of relying on from-scratch end-to-end training, which had proven metric-neutral.
- Target both CTR and CVR ranking tasks with the same embedding investment.
- Accept a hybrid CPU-GPU serving topology as the cost of hosting tables larger than GPU memory.

## Stack
Pinterest ads ranking infrastructure with CPU-GPU hybrid serving for large embedding tables. Specific frameworks are not named in the source.

## Results
- 1.34% online CPC reduction.
- 2.60% CTR increase.
- Neutral end-to-end latency impact.

## Takeaways
Large embedding tables only pay off with the right initialization: multi-algorithm pretraining converted a metric-neutral capacity increase into real business gains, and a hybrid serving design made the memory footprint deployable without a latency tax.
