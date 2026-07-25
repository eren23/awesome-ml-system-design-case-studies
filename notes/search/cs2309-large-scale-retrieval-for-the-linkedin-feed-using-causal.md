---
id: cs2309
title: Large Scale Retrieval for the LinkedIn Feed using Causal Language Models
company: LinkedIn
primary_category: search
sub_category: semantic-search
year: 2025
source_url: https://arxiv.org/abs/2510.14223
tags: [llm, llama, dual-encoder, feed-retrieval, low-latency, aaai-2026, arxiv-2025]
---

# Large Scale Retrieval for the LinkedIn Feed using Causal Language Models
**LinkedIn** · 2025 · [source](https://arxiv.org/abs/2510.14223)

## Problem
The LinkedIn Feed suggests content from beyond a member's network, which requires retrieving roughly 2,000 candidates from hundreds of millions of items within a few milliseconds at several thousand QPS. Existing dense retrieval struggled to maintain quality at this latency and scale — especially for newer members who lack an established network to draw signals from.

## Approach / System design
LinkedIn fine-tuned Meta's LLaMA 3 as a dual encoder: one tower embeds members, the other embeds content, using only textual input for both. The work spans prompt design for representing users and items as text, large-scale fine-tuning techniques, and a low-latency online serving stack that runs embedding-based retrieval at thousands of QPS with millisecond budgets.

## Key decisions
- Use a causal LLM (LLaMA 3) as the backbone of a dual encoder rather than a conventional dense retrieval model, betting on its text understanding.
- Represent everything as text via prompt design; notably, quantizing numerical features into the prompt lets that information encode properly into the embedding and improves alignment between the retrieval and ranking layers.
- Engineer serving for strict production constraints: few-millisecond retrieval from hundreds of millions of candidates at several thousand QPS.

## Stack
Fine-tuned LLaMA 3 dual encoder over textual prompts; large-scale fine-tuning pipeline; low-latency online embedding retrieval serving infrastructure. Further details are not covered in the source.

## Results
Offline metrics and online A/B tests showed substantial improvements in member engagement, with significant gains among newer members. Specific numeric lifts are not stated in the source.

## Takeaways
LLMs can power industrial-scale retrieval, not just ranking or generation, when adapted carefully: a fine-tuned causal LM dual encoder outperformed prior dense retrievers, and small representational choices (like quantizing numeric features into text) materially affect what the embedding captures. The approach particularly helps cold-start-ish users where behavioral signal is thin.
