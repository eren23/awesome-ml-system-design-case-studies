---
id: cs2360
title: "Powering Job Search at Scale: LLM-Enhanced Query Understanding in Job Matching Systems"
company: LinkedIn
primary_category: search
sub_category: query-understanding
year: 2025
source_url: https://arxiv.org/abs/2509.09690
tags: [llm, query-understanding, job-search, query-rewriting, intent-classification, entity-extraction]
---

# Powering Job Search at Scale: LLM-Enhanced Query Understanding in Job Matching Systems
**LinkedIn** · 2025 · [source](https://arxiv.org/abs/2509.09690)

## Problem
Job-search queries are short, ambiguous, and context-dependent, yet traditional job-search query understanding relies on a fragmented collection of task-specific NER models. That architecture is brittle, expensive to maintain, and slow to adapt as job taxonomies and language patterns evolve.

## Approach / System design
LinkedIn replaces the multi-model NER pipeline with a unified LLM-based query understanding framework. The LLM jointly models the user's query together with contextual signals such as profile attributes, and emits structured facet interpretations (intent, entities, expansions) that drive downstream matching and ranking. The framework is deployed in the production job-search platform and validated through online A/B testing.

## Key decisions
- One unified LLM framework instead of many task-specific NER/intent models, trading per-task specialization for maintainability and adaptability.
- Personalization at the query-understanding layer: profile attributes are fused with the query text when producing interpretations.
- Structured outputs (facet interpretations) as the contract with downstream retrieval/ranking, keeping the rest of the stack unchanged.

## Stack
Not covered in the source beyond the LLM-based framework itself (model specifications were not detailed in the abstract).

## Results
Online A/B tests showed relevance improvements, alongside reduced system complexity and lower operational overhead compared with the previous multi-model approach. Specific metric values are not given in the fetched source.

## Takeaways
For query understanding in dynamic domains, consolidating fragmented task-specific models into one LLM framework pays off twice: better interpretations (context-aware, personalized) and a dramatically simpler system to operate and evolve. Structured output is the key to slotting an LLM into an existing search stack.
