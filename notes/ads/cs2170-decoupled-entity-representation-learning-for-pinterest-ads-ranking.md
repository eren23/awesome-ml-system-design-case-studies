---
id: cs2170
title: Decoupled Entity Representation Learning for Pinterest Ads Ranking
company: Pinterest
primary_category: ads
sub_category: ctr-prediction
year: 2025
source_url: https://arxiv.org/abs/2509.04337
tags: [entity-representation, multi-tower, dhen, ads-ranking, decoupled-learning, recsys]
---

# Decoupled Entity Representation Learning for Pinterest Ads Ranking
**Pinterest** · 2025 · [source](https://arxiv.org/abs/2509.04337)

## Problem
Pinterest's ads and content personalization depend on high-quality user and Pin embeddings built from many heterogeneous data sources. Computing rich representations inside every downstream ranking model is neither scalable nor consistent across tasks.

## Approach / System design
An upstream-downstream paradigm that decouples representation learning from ranking. Upstream models train on extensive, varied signals with complex architectures (multi-tower, DHEN-backbone per the catalog metadata) to capture user–Pin relationships. The resulting embeddings are not computed in real time; they are learned offline and regularly refreshed asynchronously, then served as pre-computed features to downstream consumers — ad retrieval and CTR/CVR ranking models.

## Key decisions
- Asynchronous decoupling: precompute and refresh embeddings upstream instead of on-demand computation inside serving-path models.
- Invest architectural complexity in the upstream models, where latency constraints are relaxed, and keep downstream rankers lean.
- One shared embedding space feeding multiple downstream tasks (retrieval, CTR, CVR) for consistency and reuse.

## Stack
Multi-tower upstream models with a DHEN backbone feeding Pinterest's production ads ranking stack. Specific frameworks/infrastructure are not detailed in the source. Accepted at RecSys 2025.

## Results
The source reports notable offline and online performance improvements from production deployment, without stating specific numbers.

## Takeaways
Decoupling entity representation learning from ranking lets a platform spend model capacity where latency allows and amortize it across every downstream task — well-built embedding infrastructure lifts multiple objectives at once at production scale.
