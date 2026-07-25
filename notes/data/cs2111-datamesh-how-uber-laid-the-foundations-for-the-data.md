---
id: cs2111
title: "DataMesh: How Uber laid the foundations for the data lake cloud migration"
company: Uber
primary_category: data
sub_category: data-pipeline
year: 2024
source_url: https://www.uber.com/us/en/blog/datamesh/
tags: [data mesh, cloud migration, GCP, data governance, domain ownership, infrastructure-as-code]
---

# DataMesh: How Uber laid the foundations for the data lake cloud migration
**Uber** · 2024 · [source](https://www.uber.com/us/en/blog/datamesh/)

## Problem
Uber had to migrate 1.5 exabytes of on-prem HDFS to Google Cloud while serving 10,000+ active users, 500K daily Presto queries, and 370K daily Spark applications. The hard parts: GCS storage and IAM policy limits that could become quota bottlenecks; access control without privilege escalation under cloud-provider constraints; over 100,000 workflows with hard-coded HDFS paths scattered through millions of lines of code; and an organizational anti-pattern where ingestion teams brokered access requests instead of data owners controlling their own resources.

## Approach / System design
DataMesh is a cloud resource management service that organizes data hierarchically along organizational lines, following data-mesh principles. Its abstraction layer defines Domains (organizational units), Domain Resources (GCP projects), Data Collections (logical containers), Domain Storage (buckets with unified policies), and Data Products (curated datasets). Automated reconciliation workflows — event-triggered and scheduled — continuously align actual cloud configuration with desired state. Ownership-based mapping of data to cloud resources enables decentralized control and clean cost attribution. A Path Translation Service (PTS) rewrites hard-coded on-prem paths to cloud destinations at runtime, and a logical file system layer keeps physical bucket paths out of user code.

## Key decisions
- Vendor-neutral abstractions over direct cloud APIs, preserving future provider flexibility.
- Heuristic ownership detection (creator org, bucket location) for assets with no explicit owner.
- Intelligent data placement: heavily used tables get separate buckets to dodge GCS IOPS throttling and improve observability.
- Metadata-driven governance through integration with uOwn (ownership) and uMetadata (schema/lineage/criticality).
- Non-disruptive migration: automatic path translation instead of asking teams to rewrite paths.

## Stack
Google Cloud Platform (GCS, Storage Transfer Service), Apache Hadoop, Hive, Presto, Apache Spark, uOwn and uMetadata as metadata sources, plus custom cost/usage tracking at org, bucket, and table levels.

## Results
No specific migration or performance metrics are reported; the article positions DataMesh as the organizational and control-plane backbone that made the exabyte-scale migration tractable.

## Takeaways
Organizing cloud infrastructure around ownership boundaries simplifies management at enterprise scale and removes intermediary bottlenecks. Abstraction layers (logical file system, path translation) both prevent lock-in and eliminate the migration's biggest friction — touching 100K+ workflows. Cloud quotas need proactive placement strategy, not reactive firefighting.
