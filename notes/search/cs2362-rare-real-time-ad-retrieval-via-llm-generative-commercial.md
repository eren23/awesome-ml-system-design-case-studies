---
id: cs2362
title: "RARE: Real-time Ad Retrieval via LLM-generative Commercial Intention for Sponsored Search Advertising"
company: Tencent
primary_category: search
sub_category: retrieval
year: 2025
source_url: https://arxiv.org/abs/2504.01304
tags: [llm, ad-retrieval, sponsored-search, commercial-intention, real-time-inference]
---

# RARE: Real-time Ad Retrieval via LLM-generative Commercial Intention for Sponsored Search Advertising
**Tencent** · 2025 · [source](https://arxiv.org/abs/2504.01304)

## Problem
LLM-based generative retrieval for sponsored search struggles to scale: numeric or content-based document IDs create inefficient one-to-few mappings between generated identifiers and ads, and extracting content representations is slow — limiting coverage over large ad corpora under real-time constraints.

## Approach / System design
RARE introduces "Commercial Intentions" (CIs) as an intermediate semantic layer: an LLM customized with commercial domain knowledge generates CI text for the incoming query, and each CI maps to many ads. Retrieval then goes query → LLM-generated CIs → ads, giving richer intent matching than ID-based generation while keeping the mapping efficient. The system runs in Tencent's production sponsored-search advertising, processing hundreds of millions of search queries daily in real time.

## Key decisions
- Text-based semantic representations (CIs) instead of numeric/document IDs as the LLM's generation target.
- Inject commercial domain knowledge into the LLM so generated intentions reflect advertiser semantics, not just generic query understanding.
- Design CIs for many-to-one ad mapping, which is what makes the approach scale across a large corpus.
- Engineer the pipeline for real-time query-time inference at production traffic volumes.

## Stack
A domain-customized LLM for commercial-intention generation, integrated into Tencent's real-world online sponsored-search retrieval system. Further infrastructure details are not given in the source.

## Results
- +5.04% consumption (spend) and +6.37% Gross Merchandise Volume online.
- +1.28% CTR and +5.29% shallow conversions.
- Offline, outperformed ten competitive baselines across four major categories.

## Takeaways
The retrieval bottleneck for generative ads wasn't the LLM, it was the target vocabulary: generating human-readable commercial intentions that fan out to many ads made LLM-generative retrieval both scalable and commercially effective, lifting revenue and engagement metrics simultaneously in production.
