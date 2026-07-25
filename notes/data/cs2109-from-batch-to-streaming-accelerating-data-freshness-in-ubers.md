---
id: cs2109
title: "From Batch to Streaming: Accelerating Data Freshness in Uber's Data Lake"
company: Uber
primary_category: data
sub_category: data-pipeline
year: 2025
source_url: https://www.uber.com/us/en/blog/from-batch-to-streaming-accelerating-data-freshness-in-ubers-data-lake/
tags: [Apache Flink, streaming ingestion, data lake, Apache Hudi, real-time, IngestionNext]
---

# From Batch to Streaming: Accelerating Data Freshness in Uber's Data Lake
**Uber** · 2025 · [source](https://www.uber.com/us/en/blog/from-batch-to-streaming-accelerating-data-freshness-in-ubers-data-lake/)

## Problem
Uber's data lake was fed by batch ingestion with multi-hour freshness delays, which capped experimentation and analytics velocity. The batch jobs also burned hundreds of thousands of CPU cores daily against highly variable workloads — an expensive mismatch at petabyte scale.

## Approach / System design
IngestionNext replaces batch ingestion with a streaming architecture in three layers. The data plane consumes Kafka events with Apache Flink jobs and writes to the lake in Apache Hudi format. A control plane automates the job lifecycle (create, deploy, restart, stop, delete) and configuration management across thousands of datasets. A resilience layer provides regional failover and a fallback to batch mode during outages.

## Key decisions
- Small-file handling: replaced record-by-record Parquet merging with row-group-level merging over the columnar structure — 10x faster compaction — while enforcing schema consistency to avoid complex schema-evolution logic.
- Partition skew: operational tuning (parallelism alignment), connector fairness (round-robin polling, per-partition quotas), and skew-aware monitoring (per-partition lag metrics feeding autoscaling).
- Checkpoint synchronization: Hudi commit metadata extended to embed Flink checkpoint IDs, giving deterministic recovery during rollbacks and failovers.

## Stack
Apache Flink (stream processing), Apache Kafka (event source), Apache Hudi (lake table format), Apache Parquet (columnar storage).

## Results
Data lake freshness improved from hours to minutes-level, with a 25% reduction in compute usage relative to batch ingestion.

## Takeaways
Streaming ingestion lets freshness be treated as a first-class dimension of data quality — and can cost less than batch, not more. But minutes-level ingestion only pays off end to end once the downstream transformation and analytics layers become real-time as well.
