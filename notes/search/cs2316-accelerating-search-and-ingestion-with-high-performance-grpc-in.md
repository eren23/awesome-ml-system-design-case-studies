---
id: cs2316
title: Accelerating Search and Ingestion with High-Performance gRPC in OpenSearch
company: Uber
primary_category: search
sub_category: semantic-search
year: 2025
source_url: https://www.uber.com/us/en/blog/high-performance-grpc/
tags: [grpc, opensearch, vector-search, latency, throughput, open-source, infrastructure]
---

# Accelerating Search and Ingestion with High-Performance gRPC in OpenSearch
**Uber** · 2025 · [source](https://www.uber.com/us/en/blog/high-performance-grpc/)

## Problem
Uber's services speak Protobuf internally, but OpenSearch only exposed REST/JSON APIs. Every search and ingestion call paid for Protobuf↔JSON translation layers, adding latency, serialization overhead, and operational complexity — increasingly painful for large payloads such as high-dimensional vectors. REST/JSON was constraining how the search platform could evolve.

## Approach / System design
Uber contributed native gRPC transport to OpenSearch (landing in 3.0) as a modular layer running alongside REST on separate ports: both transports share the same internal node-to-node logic and differ only at the client-server boundary. The team prioritized the Search and Bulk APIs, and built an automated three-stage spec-to-Proto conversion pipeline (preprocessing, core conversion, postprocessing) to keep JSON and Protobuf API specifications in parity over time. On Uber's side, the Search Gateway proxy dropped its translation layers to talk gRPC end to end.

## Key decisions
- Ship gRPC as an optional module beside REST rather than a replacement, preserving compatibility for the ecosystem.
- Automate JSON-spec-to-Proto generation to prevent API drift between the two transports.
- Publish an SPI so plugins (e.g., k-NN vector search) can extend gRPC support themselves.
- Target Bulk (ingestion) and Search first, where payload size and throughput make binary transport pay off most.

## Stack
OpenSearch 3.0 with native gRPC/Protobuf transport, Uber's Search Gateway, M3 metrics stack, Spark batch ingestion jobs, k-NN vector search plugin; contributed upstream to the OpenSearch project.

## Results
Ingestion: 60% p99 write latency reduction on the M3 metrics workload (34.1ms → 13.6ms) and 34% at p50 (15.8ms → 10.5ms); 20–35% reduction in M3 Indexer max indexing delay; 20–35% faster batch Spark ingestion jobs. Search: Uber Eats recommendations saw 53% p50 (83ms → 38ms) and 43% p95 (114ms → 64ms) latency reductions. Vector workloads: 88.7% request-size reduction for 1,572-dimension vectors; gRPC SMILE format 47% faster than REST JSON.

## Takeaways
Transport/serialization choices materially shape search platform performance at scale — the wins are biggest for large binary payloads like embeddings. Contributing the transport upstream (with spec-parity tooling and extension points) let Uber remove its own translation layers while making the improvement durable across the OpenSearch ecosystem.
