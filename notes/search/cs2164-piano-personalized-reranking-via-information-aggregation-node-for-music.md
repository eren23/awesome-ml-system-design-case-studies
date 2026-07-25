---
id: cs2164
title: "PIANO: Personalized Reranking via Information Aggregation Node for Music Search Optimization"
company: NetEase Cloud Music
primary_category: search
sub_category: learning-to-rank
year: 2026
source_url: https://arxiv.org/abs/2606.16641
tags: [personalized-reranking, music-search, CTR, CVR, list-level, cross-attention, ECML-PKDD]
---

# PIANO: Personalized Reranking via Information Aggregation Node for Music Search Optimization
**NetEase Cloud Music** · 2026 · [source](https://arxiv.org/abs/2606.16641)

## Problem
Music search reranking must reconcile long-term user preferences with the immediate query while jointly optimizing CTR and CVR. Existing sequential methods cannot exploit historical search queries to surface which past preferences are relevant now, and most listwise rerankers optimize a single objective per item rather than managing multi-objective trade-offs across the whole ranked list.

## Approach / System design
PIANO is a personalized listwise reranking framework with two core components. The Query-Driven Interest Refiner (QDIR) applies cross-attention over the user's historical queries to align past intents with the current search, refining which parts of the interest history matter for this request. The Information Aggregation Node (IAN) is a learnable [CLS]-style token appended to the candidate list; it aggregates list-wide information and predicts CTR and CVR at the list level, enabling trade-off management across the entire ranking rather than item-by-item scoring.

## Key decisions
- Use historical queries — not just historical clicks — as the key to retrieving relevant past interests, via cross-attention.
- Elevate CTR/CVR from item-level predictions to list-level objectives through a single aggregation token.
- Design for listwise multi-objective optimization so click and conversion goals are balanced over the full result page.

## Stack
Transformer-style cross-attention for query-interest alignment; learnable aggregation token (IAN) for list-level prediction; evaluated on public and industrial datasets and deployed for online A/B testing on NetEase Cloud Music. Accepted at ECML-PKDD per the catalog tags.

## Results
Consistent improvements on public and industrial datasets; in online A/B tests on NetEase Cloud Music, PIANO delivered +0.62% CTR and +4.45% CVR.

## Takeaways
In search reranking, the user's query history is an underused personalization signal — attending over past queries links current intent to the right slice of long-term preference. Moving multi-objective prediction to the list level with a cheap learnable token yields outsized conversion gains relative to the architectural change involved.
