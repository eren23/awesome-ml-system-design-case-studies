---
id: cs2307
title: "UniERF: A Uniform Embedding-based Retrieval Framework for E-commerce Search"
company: JD.com
primary_category: search
sub_category: semantic-search
year: 2025
source_url: https://dl.acm.org/doi/10.1145/3711896.3737270
tags: [embedding-based-retrieval, personalization, joint-training, e-commerce, kdd-2025]
---

# UniERF: A Uniform Embedding-based Retrieval Framework for E-commerce Search
**JD.com** · 2025 · [source](https://dl.acm.org/doi/10.1145/3711896.3737270)

## Problem
Embedding-based retrieval (EBR) is a core component of industrial e-commerce search: models produce query and item representations, and approximate nearest neighbor (ANN) search retrieves relevant items. In practice, semantic relevance to the query and personalization to the individual user tend to be handled by separate models or objectives, leaving retrieval unable to jointly exploit both signals.

## Approach / System design
UniERF is a uniform embedding-based retrieval framework that incorporates diverse sample types into joint model training, so a single model learns to leverage both the semantic information of queries and the personalized features of different users. Retrieval is served through the standard EBR pattern — learned representations plus efficient ANN search — and the framework was integrated into JD.com's existing retrieval system.

## Key decisions
- Train one unified model on diverse sample types jointly, rather than maintaining separate semantic and personalized retrieval models.
- Combine query semantics with per-user personalization signals inside the same embedding space.
- Integrate into the existing JD.com retrieval system rather than replacing the serving stack.

## Stack
Embedding-based retrieval with ANN search, deployed within JD.com's production e-commerce retrieval system. Model architecture details are not covered in the accessible source (paywalled; summary based on the abstract).

## Results
Extensive offline and online experiments showed UniERF surpassing baseline methods across evaluation metrics, and it has been successfully deployed in JD.com's production retrieval system. Specific numeric lifts are not stated in the accessible source.

## Takeaways
Unifying semantic and personalized retrieval into one jointly trained embedding model avoids the fragmentation of parallel EBR stacks: diverse training samples let a single model serve both relevance and personalization, simplifying the retrieval layer while beating specialized baselines.
