---
id: cs1771
title: Ads Recommendation in a Collapsed and Entangled World
company: Tencent
primary_category: ads
sub_category: ctr-prediction
year: 2024
source_url: https://arxiv.org/abs/2403.00793
tags: [feature-encoding, dimensional-collapse, multi-task, wechat]
---

# Ads Recommendation in a Collapsed and Entangled World
**Tencent** · 2024 · [source](https://arxiv.org/abs/2403.00793)

## Problem
Tencent's large-scale ads recommendation system struggles with two representation-learning pathologies: dimensional collapse, where learned embeddings occupy far fewer effective dimensions than allocated, and interest entanglement, where user interests from different tasks or scenarios get mixed into the same representations.

## Approach / System design
The paper distills roughly a decade of production practice into a set of techniques for learning effective recommendation representations. It covers how to encode heterogeneous feature types — sequence features, numeric features, and pre-trained embedding features — into embeddings while preserving the prior knowledge each carries, plus approaches for mitigating dimensional collapse and disentangling interests across tasks and scenarios. It also describes training techniques for model optimization and bias reduction.

## Key decisions
- Treat feature encoding per type (sequence, numeric, pre-trained embedding) so prior structure is preserved rather than flattened away.
- Explicitly disentangle representations across tasks and scenarios instead of sharing one entangled space.
- Build dedicated analysis tooling — three tools for studying feature correlation, dimensional collapse, and interest entanglement — so the pathologies can be measured, not just suspected.

## Stack
Not covered in the source.

## Results
The system runs at WeChat-scale production: hundreds of billions of requests daily, serving millions of ads to billions of users. The abstract does not disclose specific metric lifts.

## Takeaways
Representation pathologies like dimensional collapse and interest entanglement are first-class production problems at ad scale, and diagnosing them requires purpose-built analysis tools; the paper's value is a decade of iterated, generalizable design principles rather than a single model.
