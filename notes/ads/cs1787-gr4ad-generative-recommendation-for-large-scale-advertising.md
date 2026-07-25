---
id: cs1787
title: GR4AD: Generative Recommendation for Large-Scale Advertising
company: Kuaishou
primary_category: ads
sub_category: targeting
year: 2026
source_url: https://arxiv.org/abs/2602.22732
tags: [generative-recommendation, autoregressive-decoding, value-aware, serving]
---

# GR4AD: Generative Recommendation for Large-Scale Advertising
**Kuaishou** · 2026 · [source](https://arxiv.org/abs/2602.22732)

## Problem
Generative recommendation is attractive for advertising, but standard LLM-style training and serving does not survive contact with a real-time ad system: ad candidates carry complex business semantics that generic tokenization misses, autoregressive decoding is too slow for multi-candidate generation under latency budgets, and next-token objectives are not aligned with ad business value.

## Approach / System design
GR4AD is a production-oriented generative recommender co-designed across architecture, learning, and serving. On tokenization, UA-SID (Unified Advertisement Semantic ID) encodes the complex business information of ads into the token space. On inference, LazyAR — a lazy autoregressive decoder — relaxes layer-wise dependencies so multiple candidates can be generated cheaply, targeting the short-sequence, many-candidate regime of ad retrieval. On optimization, Value-Aware Supervised Learning (VSL) and Ranking-Guided Softmax Preference Optimization (RSPO) align the model with business metrics; RSPO optimizes value-based rewards under list-level metrics and supports continual online updates. Serving uses dynamic beam search whose beam width adapts to generation depth and real-time system load.

## Key decisions
- Design a dedicated semantic ID scheme (UA-SID) instead of reusing generic item tokenization, so business information survives tokenization.
- Trade strict autoregressive dependencies for LazyAR's relaxed decoding, accepting the trade-off because ad generation is short-sequence and multi-candidate.
- Align training with revenue via value-aware and ranking-guided preference objectives rather than pure likelihood.
- Make beam width a runtime decision driven by depth and load, coupling model serving to system capacity.

## Stack
Autoregressive generative recommender with semantic-ID tokenization, LazyAR decoding, VSL/RSPO training objectives, and dynamic beam serving; deployed in the Kuaishou advertising system serving over 400 million users.

## Results
Large-scale A/B tests showed up to 4.2% ad revenue improvement over the existing DLRM-based stack, with consistent gains from both model scaling and inference-time scaling, while sustaining high-throughput real-time serving.

## Takeaways
Getting generative recommendation into a production ad system is a co-design problem: tokenization, decoding, training objective, and serving policy all had to be rebuilt around ad-specific constraints. Notably, both model scaling and inference-time scaling delivered gains — evidence that the scaling behaviors driving LLMs carry over to industrial ad retrieval when the architecture is adapted properly.
