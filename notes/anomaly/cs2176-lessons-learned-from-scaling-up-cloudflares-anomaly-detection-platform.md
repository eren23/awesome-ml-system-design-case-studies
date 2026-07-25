---
id: cs2176
title: Lessons Learned from Scaling Up Cloudflare's Anomaly Detection Platform
company: Cloudflare
primary_category: anomaly
sub_category: alerting
year: 2025
source_url: https://blog.cloudflare.com/lessons-learned-from-scaling-up-cloudflare-anomaly-detection-platform/
tags: [hbos, bot-detection, kafka, clickhouse, scaling, histogram-based]
---

# Lessons Learned from Scaling Up Cloudflare's Anomaly Detection Platform
**Cloudflare** · 2025 · [source](https://blog.cloudflare.com/lessons-learned-from-scaling-up-cloudflare-anomaly-detection-platform/)

## Problem
Cloudflare's anomaly detection platform flags bot traffic hiding inside legitimate-looking user behavior. The original monolithic service could not keep up as the workload grew to hundreds of thousands of requests per second across roughly 310M unique visitors, and horizontally scaling the inefficient monolith only amplified its problems.

## Approach / System design
The platform was decomposed from a single replicated service into microservices on Kubernetes with clear separation of concerns: a Baseline Service that generates site-specific behavioral profiles, a Detector Service that scores traffic, and a Publisher Service that distributes results to the edge. Events stream in via Kafka; ClickHouse holds historical data for baselines while Redis holds ephemeral per-visitor profiles with sliding windows. Detection uses Histogram-Based Outlier Scoring (HBOS), comparing visitor behavior against per-site baselines, with results pushed to the edge via Quicksilver, Cloudflare's replicated key-value store.

## Key decisions
- Chose HBOS for linear-time scoring, deliberately trading weaker local-outlier precision for fast global outlier detection at scale.
- Split storage by lifecycle: ClickHouse for durable historical baselines, Redis for short-lived visitor state.
- Added a "recency register" time-bound cache to avoid recomputing expensive detection logic, yielding a 10x throughput improvement.
- Switched from human-readable to compact binary-encoded keys, saving about 30% memory.
- Used HyperLogLog sketches for counting high-cardinality features.
- Deduplicated baseline computation, cutting ClickHouse load 10x.

## Stack
Kafka, Kubernetes, ClickHouse, Redis, HyperLogLog data structures, Quicksilver (edge KV distribution), HBOS anomaly scoring.

## Results
Scaled from 10K to 500K+ requests/second while handling ~310M unique visitors, absorbing 2x traffic growth over six months; 10x throughput gain from the recency-register cache, ~30% memory savings from binary key encoding, and 10x lower ClickHouse load from baseline deduplication.

## Takeaways
Launching a simple monolith first exposed real bottlenecks before investing in a redesign. Memory/compute trade-offs needed empirical testing — standard tuning advice didn't match their workload. Scaling out an inefficient service multiplies its inefficiencies; separating concerns let each stage be optimized independently.
