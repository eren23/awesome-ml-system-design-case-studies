---
id: cs1863
title: Uber — Apache Hudi at Uber: Engineering for Trillion-Record-Scale Data Lake Operations
company: Uber
primary_category: data
sub_category: data-discovery
year: 2026
source_url: https://www.uber.com/us/en/blog/apache-hudi-at-uber/
tags: [apache-hudi, data-lake, upserts, record-index, metadata-table, streaming-ingestion]
---

# Uber — Apache Hudi at Uber: Engineering for Trillion-Record-Scale Data Lake Operations
**Uber** · 2026 · [source](https://www.uber.com/us/en/blog/apache-hudi-at-uber/)

## Problem
Uber's data lake must support upserts, deletes, and incremental queries at a scale of trillions of records across tens of thousands of datasets. Traditional data lake formats designed for append-only batch workloads cannot efficiently handle the mutation patterns required by operational data pipelines, and metadata management becomes a scalability bottleneck at this record volume.

## Approach / System design
Uber runs Apache Hudi as the table format powering its data lake, managing 19,500 datasets and processing approximately 6 trillion row operations per day. The Metadata Table centralizes file and partition metadata to avoid expensive file-listing operations at scale. The Record Index enables efficient point-lookups during upserts for trillion-row tables without full scans. HiveSync provides cross-datacenter replication of table metadata, and the platform integrates with Apache Spark, Apache Flink, and Presto for compute.

## Key decisions
Building the Record Index specifically for trillion-scale upserts was a significant engineering investment, but necessary to keep upsert latency from growing linearly with table size. Using the Metadata Table to replace distributed file listings solved a long-standing bottleneck where Hive metastore operations became the slowest step in large table writes.

## Stack
Apache Hudi, Apache Spark, Apache Flink, Presto, Hive Metastore.

## Results
Uber manages 19,500 datasets and processes approximately 6 trillion row operations per day with Apache Hudi.

## Takeaways
At trillion-record scale, the metadata layer—not the data files—often becomes the primary performance bottleneck; dedicated solutions like Hudi's Metadata Table and Record Index are necessary to maintain acceptable operation latency. Deep integration with multiple query engines (Spark, Flink, Presto) is essential for a data lake platform serving diverse workloads simultaneously.
