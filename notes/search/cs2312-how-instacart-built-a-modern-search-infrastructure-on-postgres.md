---
id: cs2312
title: How Instacart Built a Modern Search Infrastructure on Postgres
company: Instacart
primary_category: search
sub_category: semantic-search
year: 2025
source_url: https://tech.instacart.com/how-instacart-built-a-modern-search-infrastructure-on-postgres-c528fa601d54
tags: [pgvector, postgresql, hybrid-search, elasticsearch-migration, vector-search, infrastructure]
---

# How Instacart Built a Modern Search Infrastructure on Postgres
**Instacart** · 2025 · [source](https://tech.instacart.com/how-instacart-built-a-modern-search-infrastructure-on-postgres-c528fa601d54)

## Problem
Instacart's search serves billions of items across thousands of retailers, with billions of daily partial updates for pricing and inventory. The original Elasticsearch setup buckled under this write load — indexing bottlenecks degraded read performance — and adding semantic search meant running a separate FAISS system alongside full-text search, which caused overfetching/post-filtering problems and heavy operational burden from keeping two retrieval systems in sync.

## Approach / System design
The architecture evolved in four phases: (1) full-text search on Elasticsearch, (2) migration of text retrieval to PostgreSQL, (3) semantic search added via FAISS, and (4) unification of lexical and embedding-based retrieval in PostgreSQL using the pgvector extension. The final system is a single Postgres datastore doing hybrid recall — full-text ranking (ts_rank) plus ANN vector search — with attribute-based filtering (e.g., real-time availability) applied as pre-filtering in the same query, eliminating separate indexing pipelines.

## Key decisions
- Bet on Postgres + pgvector over standalone vector databases because Instacart already ran Postgres at scale and could reuse existing operational expertise and infrastructure.
- Use a normalized data model instead of Elasticsearch-style denormalization, cutting write workload 10x.
- Build hybrid indexes keyed on retailer characteristics rather than maintaining hundreds of per-retailer indexes.
- Push computation into the database layer instead of the application layer, roughly doubling performance.
- Validate offline with production traffic patterns before cutover to confirm the new stack could handle Instacart scale.

## Stack
PostgreSQL as the unified datastore; pgvector for ANN vector search; ts_rank for text ranking; bi-encoder embeddings (MiniLM-L3-v2); real-time availability data used for pre-filtering.

## Results
- 10x reduction in write workload versus the previous architecture.
- 6% drop in searches returning zero results after the pgvector migration.
- Substantial increase in incremental revenue attributed to improved recall.
- ~2x performance gains from pushing compute to the database layer.

## Takeaways
Consolidating lexical and vector retrieval into one boring, well-understood datastore beat operating specialized systems side by side: less infrastructure, 10x less write amplification, and better search quality. Choosing technology the team already operates at scale — and prototyping against real traffic before migrating — de-risked the consolidation.
