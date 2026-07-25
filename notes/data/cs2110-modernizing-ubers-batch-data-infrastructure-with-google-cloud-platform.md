---
id: cs2110
title: Modernizing Uber's Batch Data Infrastructure with Google Cloud Platform
company: Uber
primary_category: data
sub_category: data-pipeline
year: 2024
source_url: https://www.uber.com/us/en/blog/modernizing-ubers-data-infrastructure-with-gcp/
tags: [GCP, HDFS, cloud migration, Apache Spark, data lake, Presto, object storage]
---

# Modernizing Uber's Batch Data Infrastructure with Google Cloud Platform
**Uber** · 2024 · [source](https://www.uber.com/us/en/blog/modernizing-ubers-data-infrastructure-with-gcp/)

## Problem
Uber runs one of the world's largest Hadoop installations — over an exabyte of data across tens of thousands of servers in two regions. The aging on-prem batch analytics infrastructure needed modernization to keep up with data growth, while thousands of dependent users and pipelines demanded that stability not be sacrificed during the transition.

## Approach / System design
The migration is phased to minimize user disruption. Phase 1 (IaaS) moves data lake storage to Google Cloud Storage while replicating the existing on-prem software stack on cloud infrastructure as-is. Phase 2 (PaaS) then adopts cloud-native services such as Dataproc and BigQuery for elasticity. Abstraction layers shield users from implementation details: a standardized HDFS client with a path translation service makes GCS transparent to existing workloads, and federated data-access proxies for Presto, Spark, and Hive route queries between on-prem and cloud clusters during testing and migration.

## Key decisions
- Use the Hadoop FileSystem interface compatibility layer over GCS so existing Spark/Presto/Hive workloads run unchanged.
- Standardize on open formats and engines (Apache Parquet, Hudi, Spark, Presto SQL) to minimize migration friction.
- Build on Uber's existing cloud-agnostic container and deployment infrastructure rather than starting fresh.
- Apply data-mesh principles for hierarchical cloud resource organization.

## Stack
Apache Spark, Hadoop YARN, Presto, Hive, Kubernetes, Google Cloud Platform (GCS, Dataproc, BigQuery).

## Results
No quantitative results stated — this is the strategy announcement for the migration.

## Takeaways
For migrations of this size, user transparency via abstraction (path translation, federated proxies) is the core design principle. Governance issues — cost management, non-analytics HDFS usage — should be anticipated up front, and "unknown unknowns" are best surfaced through early end-to-end integration testing plus aggressive deprecation of legacy patterns.
