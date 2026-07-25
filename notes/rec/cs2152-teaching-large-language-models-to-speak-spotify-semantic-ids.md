---
id: cs2152
title: "Teaching Large Language Models to Speak Spotify: Semantic IDs for LLM-Powered Personalization"
company: Spotify
primary_category: rec
sub_category: personalization
year: 2025
source_url: https://research.atspotify.com/2025/11/teaching-large-language-models-to-speak-spotify-how-semantic-ids-enable
tags: [LLM, semantic-ids, personalization, catalog-representation, generative, foundation-model]
---

# Teaching Large Language Models to Speak Spotify: Semantic IDs for LLM-Powered Personalization
**Spotify** · 2025 · [source](https://research.atspotify.com/2025/11/teaching-large-language-models-to-speak-spotify-how-semantic-ids-enable)

## Problem
Off-the-shelf LLMs know nothing about Spotify's catalog structure, content relationships, or user behavior. Representing tracks, podcasts, and audiobooks as plain text is noisy, inconsistent, and loses fine-grained relational structure, which makes text-only LLM personalization ineffective at catalog scale across heterogeneous content types.

## Approach / System design
Spotify built Semantic IDs: discrete, catalog-native tokens that encode content and its relationships, giving the LLM a native vocabulary for the catalog. Item embeddings are built from both textual signals (titles, descriptions, transcripts) and behavioral signals (co-listening patterns), then quantized into discrete token sequences via residual Lookup-Free Quantization. An open-weight LLM is fine-tuned on mixed text + Semantic ID data across multiple tasks (episode recommendation, search, playlist generation, user understanding), with a serving path that translates catalog URIs to Semantic IDs and back.

## Key decisions
- Fuse text and behavioral signals in the item representation instead of relying on either alone.
- Separate representation spaces per modality: text-rich content (podcasts, audiobooks) and audio-driven content (music) get type-specific quantizers over shared backbones.
- Freeze the core LLM weights and train only the new Semantic ID embeddings during alignment, preserving pretrained knowledge while learning cross-modal reasoning.
- Multi-task fine-tuning with synthetic data to avoid catastrophic forgetting and single-task overfitting.
- Pick a 1B-parameter model as the capability/efficiency sweet spot for serving.

## Stack
1B-parameter open-weight LLM; residual Lookup-Free Quantization for tokenization; vLLM with beam search for inference; Redis-backed key-value store for URI-to-Semantic-ID translation.

## Results
Episode recommendation improved 1.96x over baselines. Multi-task training beat single-task by 22%. LLM-based cleanup of item descriptions added a 5.4% accuracy gain. Scaling from 0.5B to 8B parameters yielded 16% gains on the search task. Semantic search matched production models overall with notable gains on broad-intent queries.

## Takeaways
Giving an LLM a catalog-native vocabulary beats forcing the catalog into natural language: domain-specific discrete tokens make personalization tasks tractable for a relatively small model. Careful alignment (partial freezing, multi-task mixes) is what keeps the pretrained model's general ability intact while it learns the new "language," and the same representation serves recommendations, search, and explainability.
