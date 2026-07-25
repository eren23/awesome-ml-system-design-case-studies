---
id: cs1775
title: TWIN V2: Scaling Ultra-Long User Behavior Sequence Modeling for Enhanced CTR Prediction at Kuaishou
company: Kuaishou
primary_category: ads
sub_category: ctr-prediction
year: 2024
source_url: https://arxiv.org/abs/2407.16357
tags: [ultra-long-sequence, clustering, ctr, user-behavior]
---

# TWIN V2: Scaling Ultra-Long User Behavior Sequence Modeling for Enhanced CTR Prediction at Kuaishou
**Kuaishou** · 2024 · [source](https://arxiv.org/abs/2407.16357)

## Problem
Kuaishou wants CTR models to see a user's full life-cycle behavior — sequences reaching 10^6 items — because long-term history reveals interests that recent behavior misses. Existing long-sequence approaches like SIM and the original TWIN use two-stage retrieve-then-score pipelines that become inefficient at this scale and cannot adequately capture comprehensive long-term interests.

## Approach / System design
TWIN V2 takes a divide-and-conquer route: compress the life-cycle sequence offline, then attend over the compressed form online. Hierarchical clustering groups items with similar characteristics in a user's history during offline processing, shrinking sequences from 10^5+ scale to sizes manageable for online serving while preserving the diversity of interests. Online, a cluster-aware target attention mechanism extracts multi-faceted long-term interests from the cluster representations. The proven two-stage structure (General Search Unit for retrieval, Exact Search Unit for scoring) is retained, but now operates over compressed cluster representations, with cluster sizes constrained for efficient retrieval.

## Key decisions
- Compress behavior history via offline hierarchical clustering instead of trying to attend over raw million-item sequences online.
- Make attention cluster-aware so the compression does not blur distinct interest facets.
- Keep the existing two-stage GSU/ESU architecture and slot compression underneath it, minimizing disruption to the deployed system.

## Stack
Offline hierarchical clustering pipeline feeding a cluster-aware target-attention CTR model within the TWIN two-stage framework, running in Kuaishou's production recommendation serving stack. Accepted at CIKM 2024.

## Results
Positive offline results on a multi-billion-scale industrial dataset, effectiveness confirmed in online A/B tests, and full deployment to primary traffic serving hundreds of millions of daily active users. Specific metric lifts are not given in the source abstract.

## Takeaways
The path to million-length behavior modeling was not a bigger attention mechanism but a representation change: cluster offline, attend online. Compressing life-cycle history into constrained clusters keeps online cost flat while widening the model's view of the user by orders of magnitude — and doing it inside the existing two-stage framework made it deployable at Kuaishou's scale.
