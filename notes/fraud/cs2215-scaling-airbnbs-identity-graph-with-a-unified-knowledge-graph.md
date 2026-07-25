---
id: cs2215
title: Scaling Airbnb's Identity Graph with a Unified Knowledge Graph Infrastructure
company: Airbnb
primary_category: fraud
sub_category: identity
year: 2026
source_url: https://medium.com/airbnb-engineering/scaling-airbnbs-identity-graph-with-a-unified-knowledge-graph-infrastructure-ebac467b7836
tags: [graph, knowledge-graph, janusgraph, dynamodb, identity, fraud-detection]
---

# Scaling Airbnb's Identity Graph with a Unified Knowledge Graph Infrastructure
**Airbnb** · 2026 · [source](https://medium.com/airbnb-engineering/scaling-airbnbs-identity-graph-with-a-unified-knowledge-graph-infrastructure-ebac467b7836)

## Problem
Airbnb's fraud-detection identity graph grew to 7 billion nodes and 11 billion edges, with 5 million new edges added daily. Typical queries traverse 4-8 hops, and high-fanout nodes caused disproportionate P95/P99 latency; resource-heavy queries destabilized the whole system. Meanwhile graph usage across the company was fragmented — SQL-based graphs, offline warehouse copies, DIY open-source deployments, and a vendor-locked third-party SaaS graph database adopted in 2021.

## Approach / System design
Airbnb replaced the third-party SaaS with an internally managed, paved-path multi-tenant knowledge-graph platform: JanusGraph (with Apache TinkerPop/Gremlin) on a DynamoDB storage backend, with OpenSearch for indexing. Tenants get isolated namespaces under centralized governance. Engine-side optimizations included a custom transaction strategy using DynamoDB conditional writes to cut locking overhead, parallelized `getMultiSlices` execution for high-fanout reads, and integrated distributed tracing. Client-side, queries were rewritten for the new engine — removing Path steps that trigger non-batched backend queries and optimizing side-effect aggregations — while keeping semantics equivalent.

## Key decisions
- Build on JanusGraph specifically for its pluggable storage backend: DynamoDB provides scalability now, and the storage layer can evolve independently later.
- Consolidate fragmented team-by-team graph solutions onto one multi-tenant platform instead of continuing per-team stacks.
- Take operational ownership in-house, trading vendor convenience for control over incidents, tuning, and roadmap.
- Optimize on both sides of the API — engine internals and client query patterns — rather than engine tuning alone.

## Stack
JanusGraph, Apache TinkerPop, Gremlin, Amazon DynamoDB (storage backend), OpenSearch (indexing), distributed tracing integration.

## Results
The internal platform outperformed the vendor across all query patterns, with significant P99 latency reduction (the manifest cites a 49% P99 read-latency cut), a 10x write-QPS improvement in load tests, elimination of the periodic manual instance reboots the vendor required, and faster, more transparent incident resolution. The graph continues ingesting ~5M edges/day.

## Takeaways
At sufficient scale, owning graph infrastructure beats renting it: a standardized platform reduces fragmentation, storage abstraction preserves future flexibility, and query optimization must happen at both engine and client layers. The identity graph now anchors broader knowledge-graph adoption at Airbnb — fraud detection, inventory graphs, and data lineage.
