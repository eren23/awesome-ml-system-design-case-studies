---
id: cs2174
title: "GRAB: An LLM-Inspired Sequence-First Click-Through Rate Prediction Modeling Paradigm"
company: Baidu
primary_category: ads
sub_category: ctr-prediction
year: 2026
source_url: https://arxiv.org/abs/2602.01865
tags: [llm, sequence-modeling, ctr-prediction, generative-ranking, ads, production-deployment]
---

# GRAB: An LLM-Inspired Sequence-First Click-Through Rate Prediction Modeling Paradigm
**Baidu** · 2026 · [source](https://arxiv.org/abs/2602.01865)

## Problem
Traditional deep learning recommendation models (DLRMs) for CTR prediction hit limits in generalization and long-sequence modeling, and face performance/efficiency bottlenecks. Baidu wanted the scaling behavior that LLMs exhibit — where more sequence length yields predictable gains — inside its production ads ranking.

## Approach / System design
GRAB is an end-to-end generative, sequence-first framework for CTR prediction. User interactions are treated as token-like sequences, following LLM modeling principles rather than the traditional discriminative feature-interaction paradigm. A Causal Action-aware Multi-channel Attention (CamA) mechanism captures temporal dynamics and action signals in user behavior sequences, modeling causal relationships between user actions. The system is deployed at full scale for online serving in Baidu's ads.

## Key decisions
- Sequence-first paradigm: model user behavior as ordered sequences, analogous to LLM token processing.
- Generative rather than discriminative CTR framing, importing LLM scaling properties into ranking.
- Custom CamA attention to make the attention mechanism aware of action types and causality, not just item co-occurrence.

## Stack
LLM-inspired generative ranking architecture with the CamA attention mechanism; deployed in Baidu's production ads serving. No further infrastructure details given in the source.

## Results
- +3.05% revenue and +3.49% CTR in production.
- Monotonic, approximately linear improvement as longer interaction sequences are used — an LLM-like scaling property.

## Takeaways
LLM architectural ideas (sequence modeling, scaling laws) transfer to industrial CTR prediction: a generative sequence-first design both beat the DLRM baseline in revenue/CTR and showed predictable gains from longer sequences, giving a clear scaling knob for future investment.
