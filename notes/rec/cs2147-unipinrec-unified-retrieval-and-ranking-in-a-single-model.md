---
id: cs2147
title: UniPinRec: Unified Retrieval and Ranking in a Single Model at Pinterest
company: Pinterest
primary_category: rec
sub_category: candidate-generation
year: 2026
source_url: https://arxiv.org/abs/2606.00422
tags: [unified-model, retrieval, ranking, latency, throughput, production, generative, generative-retrieval, ANN, cross-attention]
---

# UniPinRec: Unified Retrieval and Ranking in a Single Model at Pinterest
**Pinterest** · 2026 · [source](https://arxiv.org/abs/2606.00422)

## Problem
Retrieval and ranking are trained as separate models even though both are large transformers consuming the same user behavior data. That duplicates parameters, compute, and serving cost, and fragments the pipeline: different input formats, separate training jobs, separate serving stacks.

## Approach / System design
UniPinRec collapses retrieval and ranking into one end-to-end model. A shared transformer encodes the user's action sequence into candidate-independent representations, which feed two task heads:
- **Retrieval head:** ANN dot-product matching against the corpus.
- **Ranking head:** cross-attention over candidate slates.

Because the user-history encoding is candidate-independent, its computation is shared across both stages at serving time.

## Key decisions
- **Masked Action Modeling (MAM):** avoids interleaving sequences, enabling weight sharing without doubling context length.
- **Blended training examples:** pairs raw action sequences with impression slates so one training stream satisfies both retrieval and ranking objectives.
- **Cross-stage KV cache sharing:** the ranking stage reuses the user-history computation done for retrieval, cutting total FLOPs.
- Unified everything — input format, training stage, serving path — rather than only sharing weights.

## Stack
A single transformer with two task-specific heads (ANN dot-product retrieval, cross-attention ranking), one unified input format and training stage, deployed on Pinterest's existing serving infrastructure.

## Results
- +1% online engagement lift across core recommendation surfaces.
- 11.1% reduction in end-to-end serving latency.
- 63.6% QPS increase.

## Takeaways
- Retrieval and ranking are similar enough that maintaining two transformer stacks is mostly waste; unification pays in both quality and efficiency.
- The wins came from full-stack unification (inputs, training, serving), not just sharing model weights.
- Candidate-independent user encoding is the design trick that lets one forward pass serve two cascade stages.
