---
id: cs2124
title: "GenPage: Towards End-to-End Generative Homepage Construction at Netflix"
company: Netflix
primary_category: genai
sub_category: inference-opt
year: 2026
source_url: https://netflixtechblog.com/genpage-towards-end-to-end-generative-homepage-construction-at-netflix-77146fba8a08
tags: [recommendation, decoder-only-transformer, autoregressive, homepage, personalization, a-b-testing, latency, generative-ai, recommendations, llm-serving, inference, generative-recommendation, transformer, rl-post-training, diversity]
---

# GenPage: Towards End-to-End Generative Homepage Construction at Netflix
**Netflix** · 2026 · [source](https://netflixtechblog.com/genpage-towards-end-to-end-generative-homepage-construction-at-netflix-77146fba8a08)

## Problem
Netflix's homepage was built by a multi-stage pipeline — separate candidate generation and ranking at both row and entity level — with misaligned objectives across stages, heavy feature engineering, and friction whenever new product experiences needed support.

## Approach / System design
GenPage collapses the stack into a single decoder-only transformer: user history and request context become a tokenized prompt, and the model autoregressively generates the entire homepage — rows, entities, and layout — as a structured two-dimensional output. A domain-specific tokenizer encodes engagement history, profile, and request signals as context tokens and entities/rows as page tokens, compressing a user action that would take 16 GPT-5-tokenizer tokens into 4. Training follows an LLM recipe: pretraining via next-token prediction on historical homepage impressions with positive feedback, then post-training via either Weighted Binary Classification (token-level value prediction with entity-level rewards) or RL on page-level rewards using a reward model and the Dr. GRPO algorithm.

## Key decisions
- Custom domain tokenizer over a text tokenizer, for compute efficiency and product control.
- Untied input/output embedding weights to support different objectives (softmax pretraining, sigmoid WBC).
- Hybrid row decoding: autoregress only the first few entities per row, then fill the rest in one forward pass.
- Constrained decoding masks ineligible tokens to enforce business rules at inference.
- Multi-cadence incremental training — large passes every N days plus daily updates — to stay fresh without catastrophic forgetting.
- Cold-start handled by context injection plus semantic embedding fusion (ID embeddings combined with content embeddings) and fallback tokens for out-of-vocabulary entities.

## Stack
Decoder-only transformer at ~120M to ~900M parameters, trained on homepage impression logs; internal reward system converting user feedback to scalar entity-level rewards (page reward = sum of entity rewards); Dr. GRPO for RL post-training.

## Results
A 14-day A/B test against the mature production baseline showed statistically significant gains on the core engagement metric (p < 0.001), a 20% reduction in end-to-end serving latency, and better responsiveness to in-session signals. Offline: entity AUC rose from 0.91 to 0.92 (misranking 9% → 8%); scaling 120M → 900M parameters (~7.5x) cut WBC loss ~1.3%, while progressive context enrichment cut it ~6.9%; RL post-training increased homepage diversity without diversity being in the objective.

## Takeaways
In production regimes, enriching the prompt/context beats scaling model capacity — personalization is bottlenecked by the information available to the model. Replacing the multi-stage pipeline with one generative model improved both quality and latency, though emergent shifts in impressed-category distribution show holistic page generation needs monitoring for alignment with product goals.
