---
id: cs2313
title: "GREAT: Guiding Query Generation with a Trie for Recommending Related Search about Video at Kuaishou"
company: Kuaishou
primary_category: search
sub_category: relevance-eval
year: 2025
source_url: https://arxiv.org/abs/2507.15267
tags: [query-suggestion, trie, constrained-decoding, llm, short-video, kdd-2025, arxiv-2025]
---

# GREAT: Guiding Query Generation with a Trie for Recommending Related Search about Video at Kuaishou
**Kuaishou** · 2025 · [source](https://arxiv.org/abs/2507.15267)

## Problem
Kuaishou shows related-search query recommendations beneath short videos to help users discover content — an item-to-query (I2Q) recommendation task with little academic coverage. Existing approaches match videos to queries via embedding similarity, which lacks deep interaction between the video's semantic content and the query, hurting recommendation quality.

## Approach / System design
GREAT is an LLM-based generative framework guided by a trie. First, a query trie is built from historically high-performing queries (high exposure and high CTR). Second, the LLM is trained to generate quality queries using this trie. Third, at inference the trie constrains token-by-token decoding so the model can only emit queries that exist in the vetted query space, followed by a post-processing refinement step. The team also released KuaiRS, a large-scale dataset derived from real Kuaishou production data for video-related search.

## Key decisions
- Generate queries with an LLM instead of retrieving by embedding similarity, enabling deep semantic interaction between video content and query.
- Constrain decoding with a trie of proven queries, guaranteeing outputs are real, high-quality queries rather than hallucinated strings.
- Curate the trie from behavioral performance signals (exposure, CTR), baking real-world quality directly into both training data and the inference search space.
- Publish KuaiRS to give the I2Q task a realistic benchmark.

## Stack
LLM generator with trie-constrained decoding and post-processing refinement; query trie built from production exposure/CTR logs. Specific model and serving details are not covered in the source.

## Results
Extensive offline and online experiments demonstrated the framework's effectiveness, and it is deployed for related-search recommendations under short videos at Kuaishou. Specific numeric metrics are not stated in the source.

## Takeaways
Trie-constrained generation is a practical recipe for production LLM query suggestion: the LLM contributes semantic understanding of the video while the trie guarantees every output is a known, high-performing query — combining generative flexibility with retrieval-grade safety.
