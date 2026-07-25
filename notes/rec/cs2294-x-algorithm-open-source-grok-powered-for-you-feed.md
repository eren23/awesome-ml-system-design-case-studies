---
id: cs2294
title: "X Algorithm: Open-Source Grok-Powered For You Feed Recommendation"
company: X
primary_category: rec
sub_category: sequential-transformer
year: 2026
source_url: https://github.com/xai-org/x-algorithm
tags: [open-source, grok, transformer, for-you-feed, rust, candidate-sourcing, phoenix]
---

# X Algorithm: Open-Source Grok-Powered For You Feed Recommendation
**X** · 2026 · [source](https://github.com/xai-org/x-algorithm)

## Problem
X open-sourced the recommendation system behind its For You feed to make its ranking decisions transparent. The system's job: blend in-network posts (from followed accounts) with out-of-network discoveries surfaced by ML, ranked end-to-end rather than by hand-tuned rules.

## Approach / System design
A composable, multi-stage pipeline orchestrated by Home Mixer (a gRPC orchestration layer): (1) query hydration pulls user context — engagement history, following lists; (2) candidate sourcing from Thunder, an in-memory post store fed by Kafka for in-network content, and Phoenix Retrieval for ML-discovered out-of-network content; (3) candidate enrichment with post metadata, author, and media details; (4) pre-scoring filters removing duplicates, stale posts, blocked authors, and muted keywords; (5) scoring via Phoenix — a Grok-based transformer (adapted from xAI's open-sourced Grok-1) predicting 14+ engagement action types, combined with weights and diversity adjustments; (6) top-k selection; (7) post-selection visibility and dedup validation.

## Key decisions
- Eliminate hand-engineered features in favor of a transformer learning directly from user engagement sequences.
- Predict many engagement actions (14+) rather than a single relevance score, then combine them.
- Isolate candidates during ranking so a post's score is independent of what else is in the batch.
- Build the pipeline as composable, parallel-executable stages so components can be added modularly.

## Stack
Rust (~57%) and Python (~43%). Phoenix (Grok-based transformer for ranking and retrieval), Thunder (in-memory post store with Kafka ingestion), Home Mixer (gRPC orchestration), and a reusable candidate-pipeline framework.

## Results
No engagement or performance metrics are disclosed; the release emphasizes architectural transparency over benchmarks.

## Takeaways
The repo documents the industry shift from feature-engineered ranking to end-to-end transformer scoring over engagement sequences, and shows a production-shaped reference for the composable candidate-pipeline pattern: source, enrich, filter, score, select, validate — with the heavy ML concentrated in one Grok-derived scoring model.
