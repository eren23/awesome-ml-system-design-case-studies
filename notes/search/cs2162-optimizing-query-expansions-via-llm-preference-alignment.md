---
id: cs2162
title: Optimizing Query Expansions via LLM Preference Alignment
company: Spotify
primary_category: search
sub_category: retrieval
year: 2025
source_url: https://research.atspotify.com/2025/7/optimizing-query-expansions-via-llm-preference-alignment
tags: [query-expansion, LLM, DPO, preference-alignment, retrieval, alignment]
---

# Optimizing Query Expansions via LLM Preference Alignment
**Spotify** · 2025 · [source](https://research.atspotify.com/2025/7/optimizing-query-expansions-via-llm-preference-alignment)

## Problem
Vocabulary mismatch is a core retrieval failure: the words users type differ from the words in relevant documents (misheard lyrics are a canonical Spotify example). LLM query expansion helps, but the common generate-many-then-filter pattern is computationally expensive and slow for production search.

## Approach / System design
Aligned Query Expansion (AQE) trains the expansion model to directly emit retrieval-effective expansions, removing the filtering stage. The pipeline: (1) generate multiple candidate expansions zero-shot; (2) score each candidate by where the relevant document ranks when the expansion is paired with the original query — the search system itself provides the preference signal; (3) train on high-scoring vs. low-scoring expansion pairs using Rejection Sampling Fine-tuning (RSFT) combined with Direct Preference Optimization (DPO).

## Key decisions
- Use downstream retrieval rank as the preference signal, aligning generation with what actually helps the search system rather than with human notions of a good expansion.
- Shift the cost offline: align the model once so inference needs a single generation, instead of candidate fan-out plus filtering at query time.
- Combine RSFT with DPO for the alignment step.

## Stack
LLM query-expansion models trained with RSFT + DPO on retrieval-derived preference pairs; evaluated on Natural Questions and EntityQs benchmarks.

## Results
On Natural Questions, AQE reached 30.8% top-1 retrieval accuracy vs. 28.5% for generate-then-filter baselines, with roughly 70% less processing time. Out of domain on EntityQs it hit 46.7% accuracy vs. 23.7% for baselines.

## Takeaways
When a downstream system can score outputs, that score is free preference data — aligning the generator to it beats sampling-and-filtering on both quality and cost. The out-of-domain gains suggest alignment teaches the model what "retrievable" means generally, not just per-dataset tricks.
