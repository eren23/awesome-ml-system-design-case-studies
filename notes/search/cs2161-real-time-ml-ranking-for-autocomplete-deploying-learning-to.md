---
id: cs2161
title: "Real-time ML Ranking for Autocomplete: Deploying Learning-to-Rank inside OpenSearch (Part 1)"
company: Swiggy
primary_category: search
sub_category: autocomplete
year: 2026
source_url: https://medium.com/swiggybytes/real-time-ml-ranking-in-autocomplete-part-1-3cdbbd44f85a
tags: [autocomplete, learning-to-rank, OpenSearch, real-time, LTR, feature-store]
---

# Real-time ML Ranking for Autocomplete: Deploying Learning-to-Rank inside OpenSearch (Part 1)
**Swiggy** · 2026 · [source](https://medium.com/swiggybytes/real-time-ml-ranking-in-autocomplete-part-1-3cdbbd44f85a)

## Problem
Autocomplete fires on every keystroke (typing "biryani" produces 7+ requests), so it handles orders of magnitude more traffic than the main search endpoint under a sub-10ms ranking budget. Swiggy's hand-tuned heuristic scoring formula grew brittle as signals multiplied: fuzzy-match strength was hard to balance against popularity, conversion signals were not incorporated, ranking across entity types (dishes, restaurants, cuisines, brands) was inconsistent, and every adjustment meant manual retuning.

## Approach / System design
Swiggy replaced the heuristic `function_score` queries with a Learning-to-Rank model running inside OpenSearch via the LTR plugin, using a two-phase retrieve-then-rescore pipeline. Two retrieval flows share one index: a partial-match flow for ambiguous prefixes ("bi") and a semantic-template flow for clearer intent ("biryani"). The index holds precomputed behavioral signals — click counts, conversion rates, order volumes, ratings — and the LTR model rescores the top-k retrieved candidates.

## Key decisions
- Run inference inside the search engine: no external model-service call, which is what keeps keystroke-level latency viable.
- Two-phase scoring (fast retrieval, then ML rescore on top-k) bounds latency regardless of model complexity.
- Define features as Mustache templates covering both query-dependent (text match) and query-independent (ratings, popularity) signals.
- Build labels from logged behavior: log features for top-k results, join with click/order outcomes.

## Stack
OpenSearch LTR plugin (supports RankLib, XGBoost, and linear models); RankLib for offline training with LambdaMART, Random Forests, and RankNet experiments; Databricks for the training pipeline; offline evaluation via MRR and NDCG; deployment through the OpenSearch rescore API. A real-time feature store serves behavioral signals per the catalog summary.

## Results
The article reports improved ranking quality from the richer set of learned signals and better handling of ambiguity and typos, but does not publish concrete metric numbers in Part 1. Part 2 is slated to cover real-time personalization.

## Takeaways
For keystroke-scale traffic, architecture is dictated by the latency budget: in-engine inference and retrieve-then-rescore made ML ranking feasible where an external model service could not be. Historical behavior logs turned the heuristic-tuning problem into a supervised learning problem with standard LTR tooling.
