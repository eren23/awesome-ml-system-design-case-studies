---
id: cs0788
title: "Unlocking Efficient Ad Retrieval: Offline Approximate Nearest Neighbors in Pinterest Ads"
company: Pinterest
primary_category: ads
sub_category: ctr-prediction
year: 2025
source_url: https://medium.com/pinterest-engineering/unlocking-efficient-ad-retrieval-offline-approximate-nearest-neighbors-in-pinterest-ads-6fccc131ac14
tags: [ad ranking, targeting]
---

# Unlocking Efficient Ad Retrieval: Offline Approximate Nearest Neighbors in Pinterest Ads
**Pinterest** · 2025 · [source](https://medium.com/pinterest-engineering/unlocking-efficient-ad-retrieval-offline-approximate-nearest-neighbors-in-pinterest-ads-6fccc131ac14)

## Problem
Pinterest retrieves ads from a large, growing inventory using ANN. Online ANN gives real-time personalization but its infra cost and latency grow with inventory size. Even after migrating from HNSW to IVF (enabling a 10x larger index), cost remained a barrier to actually using the expanded inventory.

## Approach / System design
Add Offline ANN as a complementary retrieval mode. Instead of running the ANN search per request, query embeddings are precomputed in a batch workflow, the ANN search runs offline, and the top-K neighbors per query are written to a KV store. At serving time the online system just does an ID-based key lookup and expands the candidates — replacing an expensive online search with a cheap storage read.

Two production use cases:
- Similar Item Ads (dynamic retargeting): two-step retrieval — get a candidate list during feature expansion, then construct an ID-based retrieval query against the indexing system. Offline ANN gave lower infra cost and better engagement/conversion than the online version.
- Visual Embedding candidate generator: compute nearest neighbors for head/cached Pins offline, push predictions to a KV store, expand by exact ID match online.

## Key decisions
- Use offline ANN only where the query context is relatively static (real-time query embeddings not required); keep online ANN where real-time adaptation matters.
- Mitigate the "fixed number of neighbors" limitation by over-generating neighbors and, for Similar Item Ads, scaling up the index size (cheap for ID-based retrieval) to overcome the small post-targeting/budget candidate count.

## Stack
IVF index (migrated from HNSW); offline batch ANN workflow; KV store for precomputed neighbors; ID-based exact-match retrieval at serving time. Pinterest notes it is building its own offline ANN framework/platform with index hyperparameter tuning and recall monitoring.

## Results
- Similar Item Ads: lower infra cost plus better engagement and conversion vs online ANN.
- Visual Embedding CG: comparable recall to online ANN with tuned K; on-par CTR but much higher gCTR30; less than 50% of the online infra cost.
- General claim: offline ANN can cut infrastructure cost by up to ~80%, mainly from cheaper lookups vs search and eliminating repeated per-query ANN searches.

## Takeaways
When the query context is stable, moving ANN from request time to a batch precompute trades real-time flexibility for large cost savings and even quality gains. The recurring pattern: precompute top-K offline, store by key, and reduce online serving to an ID lookup.
