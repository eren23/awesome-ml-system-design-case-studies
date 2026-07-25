---
id: cs2151
title: QARM: Quantitative Alignment Multi-Modal Recommendation at Kuaishou
company: Kuaishou
primary_category: rec
sub_category: embeddings
year: 2024
source_url: https://arxiv.org/abs/2411.11739
tags: [multimodal, representation-alignment, short-video, production, 400M-users, visual-features]
---

# QARM: Quantitative Alignment Multi-Modal Recommendation at Kuaishou
**Kuaishou** · 2024 · [source](https://arxiv.org/abs/2411.11739)

## Problem
The standard way to use multi-modal content features in recommenders — pre-train a multi-modal model, cache its embeddings, feed them downstream — has two structural flaws:
- **Representation unmatching:** the multi-modal model is supervised by NLP/CV objectives while the recommender optimizes user-item interactions; the goals are fundamentally different, so the representations are misaligned.
- **Representation unlearning:** cached embeddings are frozen, so gradients from the recommendation model can never refine them.

## Approach / System design
QARM is a quantitative multi-modal framework that customizes specialized, trainable multi-modal representations for each downstream recommendation model, replacing the cascading pre-train → cache → use paradigm with representations that stay learnable inside the recommendation context.

## Key decisions
- Abandon frozen cached embeddings in favor of end-to-end trainable multi-modal representations.
- Customize (quantitatively align) representations per downstream model rather than sharing one universal embedding.

## Stack
Multi-modal large models as the pre-training backbone, a quantitative alignment mechanism as the core contribution, and Kuaishou's downstream recommendation models. Implementation specifics beyond this are not covered in the source abstract.

## Results
The abstract (marked "work in progress") does not disclose specific metrics. Per the catalog summary, the framework is deployed in production for short-video recommendation serving 400M+ daily active users.

## Takeaways
- Static multi-modal embeddings are structurally misaligned with recommendation objectives; alignment must be learned.
- Trainability of content representations inside the recommender loop is the key unlock, not bigger pre-trained encoders.
- Task-specific customization beats one-size-fits-all universal representations for downstream models.
