---
id: cs2150
title: OnePiece: Context Engineering and Reasoning for Cascade Ranking at Shopee
company: Shopee
primary_category: rec
sub_category: personalization
year: 2025
source_url: https://arxiv.org/abs/2509.18091
tags: [cascade-ranking, context-engineering, LLM, reasoning, personalized-search, GMV, ad-revenue]
---

# OnePiece: Context Engineering and Reasoning for Cascade Ranking at Shopee
**Shopee** · 2025 · [source](https://arxiv.org/abs/2509.18091)

## Problem
Industrial search and recommendation systems have failed to capture what actually made LLMs successful. Most efforts just transplant the Transformer architecture into ranking models, which yields only marginal gains over well-tuned traditional deep learning baselines. The missing ingredients are context engineering and multi-step reasoning.

## Approach / System design
OnePiece brings both LLM mechanisms into a cascade ranking pipeline (retrieval + ranking) on a pure Transformer backbone:
1. **Structured context engineering:** augments the raw interaction history with preference and scenario signals, and unifies everything into a structured tokenized input sequence shared by retrieval and ranking.
2. **Block-wise latent reasoning:** the model refines representations over multiple reasoning steps, with reasoning bandwidth scaled by block size.
3. **Progressive multi-task training:** user feedback chains supervise the intermediate reasoning steps, not just the final prediction.

## Key decisions
- Bet that context engineering and reasoning — not architecture swaps — are the transferable lessons from LLMs.
- Made the tokenized context format shared across retrieval and ranking stages.
- Used naturally occurring feedback chains as intermediate supervision instead of only end labels.

## Stack
Pure Transformer backbone, structured input tokenization, block-wise latent reasoning architecture, progressive multi-task training. Deployed in Shopee's production personalized search.

## Results
- +2% GMV per unique user.
- +2.90% advertising revenue increase.

## Takeaways
- Transplanting Transformers is not enough; how you construct the input context and let the model reason drives the gains.
- Latent reasoning with adjustable block size gives a tunable compute/quality knob for ranking.
- User feedback chains are a free source of supervision for intermediate reasoning steps.
