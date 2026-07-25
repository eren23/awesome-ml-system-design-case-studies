---
id: cs2149
title: GLIDE: Deploying Semantic ID-based Generative Retrieval for Podcast Discovery at Spotify
company: Spotify
primary_category: rec
sub_category: candidate-generation
year: 2026
source_url: https://arxiv.org/abs/2603.17540
tags: [generative-retrieval, semantic-ids, podcast-discovery, production, non-habitual-streaming, new-show-discovery]
---

# GLIDE: Deploying Semantic ID-based Generative Retrieval for Podcast Discovery at Spotify
**Spotify** · 2026 · [source](https://arxiv.org/abs/2603.17540)

## Problem
Podcast listening has a split personality: users keep stable favorite shows, but their discovery intent shifts over time. Traditional recommenders lean on long-term patterns and struggle to incorporate rich contextual signals or flexible, intent-aware objectives — especially under production latency and cost constraints.

## Approach / System design
GLIDE frames podcast recommendation as an instruction-following task over a discretized catalog. Shows are represented as Semantic IDs, so an LLM generates recommendations grounded in the real inventory rather than hallucinating titles. The model conditions on recent listening history and lightweight user context, and long-term user embeddings are injected as soft prompts to carry stable preferences. The whole system runs under strict inference constraints for production serving.

## Key decisions
- Semantic IDs discretize the large catalog, making generation grounded and hallucination-free.
- Long-term taste enters via soft-prompt embeddings instead of heavyweight full personalization, keeping inference cheap.
- Recent history plus lightweight context balances relevance against latency.
- Objectives support both familiarity and exploration-oriented discovery.

## Stack
LLM-based generative retrieval with Semantic ID catalog representation and user-embedding soft prompts. Base model and serving details are not covered in the source.

## Results
A/B tests across millions of users:
- Non-habitual podcast streaming up by as much as 5.4%.
- New-show discovery up by as much as 14.3%.
- Met production cost and latency constraints.

## Takeaways
- Semantic IDs are the bridge that makes LLM generation safe over a large closed inventory.
- Splitting personalization into soft-prompt long-term embeddings plus recent-context conditioning balances quality and inference cost.
- Generative retrieval specifically moved exploration metrics (non-habitual streaming, new-show discovery) — the area where classic recommenders are weakest.
