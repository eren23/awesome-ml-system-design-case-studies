---
id: cs1848
title: Pinterest — Next Generation DB Ingestion at Pinterest
company: Pinterest
primary_category: data
sub_category: data-pipeline
year: 2026
source_url: https://medium.com/pinterest-engineering/next-generation-db-ingestion-at-pinterest-66844b7153b7
tags: [change-data-capture, kafka, flink, iceberg, ingestion, debezium]
---

# Pinterest — Next Generation DB Ingestion at Pinterest
**Pinterest** · 2026 · [source](https://medium.com/pinterest-engineering/next-generation-db-ingestion-at-pinterest-66844b7153b7)

## Problem
Pinterest's existing batch-based database ingestion introduced data freshness delays of hours, making it unsuitable for analytics and ML use cases that require near-real-time views of operational data. Batch snapshots also placed heavy load on source databases during export windows and struggled to handle the scale of Pinterest's MySQL and TiDB deployments efficiently.

## Approach / System design
Pinterest replaced batch ingestion with a Change Data Capture (CDC) pipeline. Debezium captures row-level changes from MySQL, while TiCDC handles TiDB. These change events are published to Apache Kafka and then processed by Apache Flink and Apache Spark jobs that apply them to Apache Iceberg tables using merge-on-read semantics. This architecture delivers database changes to the analytics layer within minutes of them occurring in the source systems.

## Key decisions
Adopting Iceberg with merge-on-read was key to handling CDC updates efficiently without expensive full rewrites of large data files on every change. Running Flink for streaming CDC application alongside Spark for batch reconciliation gave the pipeline both low-latency updates and periodic consistency checks against the source.

## Stack
Debezium, TiCDC, Apache Kafka, Apache Flink, Apache Spark, Apache Iceberg.

## Results
Data from MySQL, TiDB, and KVStore is now available in the analytics and ML layers within minutes rather than hours.

## Takeaways
CDC-based ingestion fundamentally changes the freshness and load profile of database replication compared to batch snapshots: changes propagate continuously and source load is spread evenly over time. Iceberg's merge-on-read support is a practical enabler for CDC at scale because it decouples write amplification from query performance.
