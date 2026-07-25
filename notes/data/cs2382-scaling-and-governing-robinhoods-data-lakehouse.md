---
id: cs2382
title: Scaling and Governing Robinhood's Data Lakehouse
company: Robinhood
primary_category: data
sub_category: data-pipeline
year: 2023
source_url: https://www.onehouse.ai/blog/scaling-and-governing-robinhoods-data-lakehouse
tags: [data-lakehouse, apache-hudi, cdc, debezium, data-pipeline, petabyte-scale]
---

# Scaling and Governing Robinhood's Data Lakehouse
**Robinhood** · 2023 · [source](https://www.onehouse.ai/blog/scaling-and-governing-robinhoods-data-lakehouse)

## Problem
Robinhood's data infrastructure had to absorb exponential growth across 10,000+ data sources and multi-petabyte datasets while holding strict SLAs on data freshness, plus governance and regulatory obligations (GDPR/CCPA "right to be forgotten") — all with a lean team.

## Approach / System design
A tiered lakehouse architecture on Apache Hudi and open-source components. Workloads are separated by criticality — Tier 0 for the highest-priority processes such as fraud detection — with SLAs, resources, and freshness guarantees assigned per tier. Change Data Capture pipelines built on Debezium stream changes from relational databases through Kafka into object storage, where Spark/DeltaStreamer jobs land them in Hudi tables with near-real-time processing. Centralized metadata services track freshness, cost, access control, and compliance status across lakehouse zones, and dedicated ID Mapping and Mask-to-PII services make lakehouse-wide PII deletion efficient.

## Key decisions
- Apache Hudi as the transactional core of the lakehouse, enabling incremental, near-real-time ingestion at scale.
- Tiering by criticality so the most important pipelines (e.g., fraud detection) get the strictest SLAs and isolation.
- Metadata-driven governance: one central layer tracking freshness, costs, access, and compliance instead of per-pipeline handling.
- Purpose-built PII services (ID Mapping, Mask-to-PII) to satisfy GDPR/CCPA deletion at lakehouse scale.
- Resource isolation via dedicated Debezium connectors and Postgres replication slots to prevent single-source contention.

## Stack
Apache Hudi, Debezium (CDC), Apache Spark / DeltaStreamer, Kafka, PostgreSQL, AWS S3.

## Results
- Manages 50,000+ datasets from 10,000+ sources at petabyte scale with a lean team.
- Meets critical freshness SLAs across tiers, including Tier 0 fraud-detection pipelines.
- Achieves GDPR compliance at scale with fast lakehouse-wide PII deletion.

## Takeaways
Tiering generalizes: applying criticality tiers not just to processing but to metadata, governance, and compliance keeps a huge lakehouse manageable by a small team. CDC-based incremental ingestion with Hudi delivers near-real-time freshness at petabyte scale, and building deletion/PII plumbing as first-class services turns regulatory compliance from a scramble into routine operations.
