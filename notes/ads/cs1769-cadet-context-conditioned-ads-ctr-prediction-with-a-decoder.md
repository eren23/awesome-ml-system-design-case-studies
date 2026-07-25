---
id: cs1769
title: CADET: Context-Conditioned Ads CTR Prediction With a Decoder-Only Transformer
company: LinkedIn
primary_category: ads
sub_category: ctr-prediction
year: 2026
source_url: https://arxiv.org/abs/2602.11410
tags: [ctr, decoder-transformer, sponsored-content, rotary-embeddings]
---

# CADET: Context-Conditioned Ads CTR Prediction With a Decoder-Only Transformer
**LinkedIn** · 2026 · [source](https://arxiv.org/abs/2602.11410)

## Problem
LinkedIn's ads CTR prediction had been dominated by DLRM-style models. Moving to transformers promises better sequence modeling, but ads prediction has obstacles generic transformers do not handle: contextual signals like ad position are only known after scoring (a chicken-and-egg problem between predicted CTR and the ranking decision), offline-online consistency is easy to break with in-session leakage, and industrial workloads impose hard training and serving efficiency limits.

## Approach / System design
CADET is a decoder-only transformer with five production-motivated pieces. (1) Context-conditioned multi-tower prediction heads explicitly model post-scoring signals such as ad position, resolving the circular dependency between CTR estimates and ranking. (2) Self-gated attention adaptively regulates information flow at both the representation and interaction levels to stabilize training. (3) Timestamp-based rotary position embeddings (RoPE) encode temporal relationships spanning seconds to months rather than mere sequence order. (4) Session masking prevents the model from learning dependencies on in-session events that will not be available at serving time, closing train-serve skew. (5) Engineering for scale: tensor packing, sequence chunking, and custom Flash Attention kernels for efficient training and serving.

## Key decisions
- Handle post-scoring context (e.g., position) with dedicated conditioned towers rather than pretending it is available pre-ranking.
- Encode time with timestamp-driven RoPE so gaps between user events carry meaning across very different timescales.
- Enforce serving-time realism during training via session masking instead of patching skew after the fact.
- Invest in custom kernels and packing so the transformer meets industrial latency/throughput budgets.

## Stack
Decoder-only transformer with multi-tower heads, self-gated attention, timestamp RoPE, session masking; tensor packing, sequence chunking, and custom Flash Attention kernels; deployed on LinkedIn's ads platform for homefeed sponsored updates.

## Results
In production A/B testing, CADET delivered an 11.04% CTR lift over LiRank, LinkedIn's production baseline (a hybrid ensemble of DCNv2 and sequential encoders). It now serves main traffic for homefeed sponsored updates.

## Takeaways
The gap between a research transformer and a production ads model is a set of specific mismatches — post-scoring context, temporal structure, train-serve skew, and cost — and CADET's gains came from addressing each one directly. A double-digit CTR lift over a strong DLRM ensemble is notable evidence that decoder-only architectures can beat mature feature-interaction stacks in ads once properly conditioned.
