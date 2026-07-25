---
id: cs2315
title: The Evolution of Uber's Search Platform
company: Uber
primary_category: search
sub_category: semantic-search
year: 2025
source_url: https://www.uber.com/us/en/blog/evolution-of-ubers-search-platform/
tags: [vector-search, opensearch, semantic-search, nrt, batch-decoupling, infrastructure]
---

# The Evolution of Uber's Search Platform
**Uber** · 2025 · [source](https://www.uber.com/us/en/blog/evolution-of-ubers-search-platform/)

## Problem
Uber's search spans massive, fast-changing marketplace data — over a million restaurants with thousands of dishes per Uber Eats session, plus use cases like driver-rider matching that need true real-time query capability, which Lucene's near-real-time (NRT) semantics couldn't deliver. Maintaining a custom in-house engine meant perpetually re-implementing new Lucene features, draining resources from actual innovation.

## Approach / System design
Three phases. Pre-2019: Elasticsearch run as a black box, optimized for availability over customization. 2019–2024: Sia, a custom in-house engine with a three-layer index — a memory-resident Live Index for concurrent reads/writes on actively updating data, immutable Snapshot Index segments cut roughly every 30 minutes, and a weekly-consolidated Base Index for memory efficiency. 2024+: Project Sunrise, a strategic pivot from custom development to OpenSearch, extending it where needed (LucenePlus with custom join operators for hierarchical parent-child marketplace queries like items-within-stores) and separating read and write paths so expensive ingestion work (forced merges) can't degrade query serving.

## Key decisions
- Adopt OpenSearch over Elasticsearch/Solr for its Apache 2.0 open-source governance, avoiding vendor lock-in — Uber became a founding member of the OpenSearch Software Foundation.
- Contribute gaps back upstream (LucenePlus, gRPC/Protobuf transport) instead of forking privately.
- Read/write separation: dedicated ingestion nodes with forced merges, decoupled from query-serving nodes.
- Kafka-based pull ingestion for resilience and backpressure, and active-active cross-region deployment via Kafka replication.
- Recognize only a small subset of use cases truly needs real-time freshness, allowing NRT workloads to be decoupled from the heavyweight Sia machinery.

## Stack
OpenSearch (replacing the in-house Sia engine), gRPC with Protobuf for RPC, Apache Kafka pull-based ingestion, Apache HDFS and Google Cloud Storage for storage, LucenePlus custom join operators, and an OpenSearch-compatible Search Gateway service.

## Results
No quantitative metrics are covered in the source; the outcomes described are qualitative — sustainable platform evolution, simplified operations from decoupling NRT from batch workloads, and semantic/vector search capabilities on a community-supported engine.

## Takeaways
Custom search engines become a treadmill of Lucene re-implementation; contributing domain-specific gaps (hierarchical joins, gRPC, pull ingestion) to open source proved more sustainable. Architecturally, read/write separation and honest triage of which workloads truly need real-time freshness were the simplifications that made the migration work.
