---
id: cs2146
title: PinRec: Outcome-Conditioned Generative Retrieval for Pinterest Recommendations
company: Pinterest
primary_category: rec
sub_category: candidate-generation
year: 2025
source_url: https://arxiv.org/abs/2504.10507
tags: [generative-retrieval, semantic-ids, multi-token, candidate-generation, two-tower, production]
---

# PinRec: Outcome-Conditioned Generative Retrieval for Pinterest Recommendations
**Pinterest** · 2025 · [source](https://arxiv.org/abs/2504.10507)

## Problem
Generative retrieval approaches typically need a separate model per product surface (home feed, search, related pins), multiplying training and serving cost, and they struggle to capture how user interests evolve across an activity sequence. Pinterest wanted a single generative retriever serving heterogeneous surfaces with surface-specific business goals.

## Approach / System design
PinRec uses a pretrain-then-fine-tune recipe on transformer-based sequential models:
- **Pretraining** on aggregated user activity across all surfaces for generalization.
- **Fine-tuning** with surface-specific impression data for specialization.
- **Outcome-conditioned generation:** the decoder is conditioned on the desired outcome, so the same model can target different business objectives per surface.

This is described as the first deployed production study of outcome-conditioned, multi-token generative retrieval at Pinterest scale.

## Key decisions
- One unified model across surfaces instead of dedicated per-surface retrievers.
- Transformer-based sequential generation of candidate items rather than two-tower embedding lookup.
- Outcome conditioning to align generations with each surface's objective.
- Hybrid training (cross-surface pretraining + surface fine-tuning) to balance generalization and specialization.

## Stack
Transformer-based sequential modeling; pretraining/fine-tuning pipeline; production deployment in Pinterest's recommendation serving. Further infrastructure detail is not covered in the source.

## Results
- +4% increase in search saves (the primary disclosed online metric).
- Reported improvements across performance, diversity, and efficiency dimensions.

## Takeaways
- Unified generative retrieval is viable in production at large scale when pretraining and fine-tuning are split across generality and surface specificity.
- Conditioning generation on outcomes is a clean way to serve heterogeneous business goals from one model.
- A single-model approach can match or beat multi-model baselines while cutting system complexity.
