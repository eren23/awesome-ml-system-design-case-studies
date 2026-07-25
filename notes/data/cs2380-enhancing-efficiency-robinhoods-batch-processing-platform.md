---
id: cs2380
title: "Enhancing Efficiency: Robinhood's Batch Processing Platform"
company: Robinhood
primary_category: data
sub_category: data-pipeline
year: 2023
source_url: https://robinhood.com/us/en/newsroom/robinhoods-batch-processing-platform/
tags: [batch-processing, data-pipeline, ml-infrastructure, etl, fintech]
---

# Enhancing Efficiency: Robinhood's Batch Processing Platform
**Robinhood** · 2023 · [source](https://robinhood.com/us/en/newsroom/robinhoods-batch-processing-platform/)

## Problem
Robinhood's V1 Hadoop-based batch system couldn't keep up with operational demands. Users had to log into development gateway machines to test jobs — inconvenient and a security concern. Job submission was inflexible, forcing workarounds for diverse use cases (audience targeting, IPO allocations, fraud testing, ML operations), and multi-cluster management overhead drove up costs and limited scaling.

## Approach / System design
Robinhood built a V2 platform around a Job Management Service (JMS) — an abstraction layer over job submission that enabled migrating workloads from Hadoop to Kubernetes without exposing users to the underlying change. The migration was fault-tolerant with automatic fallback to the old path, and a separate Spark Control Plane isolates batch workloads from the main K8s cluster. Spark jobs run on Kubernetes via the Spark-K8s Operator using custom resource definitions, orchestrated with Airflow.

## Key decisions
- Adopted the Spark-K8s Operator with CRDs as the execution model on Kubernetes.
- Sharded the operator after hitting processing delays beyond roughly 3,000 Spark pods.
- Imposed namespace service limits to avoid Kubernetes service-discovery issues.
- Enforced TTLs on Spark custom resources to protect etcd reliability.
- Deployed across multiple AZs and K8s clusters for high availability, and routed batch jobs onto spare K8s capacity overnight for cost efficiency.

## Stack
Apache Spark, Hadoop (legacy), Kubernetes, Spark-K8s Operator, Apache Airflow, AWS S3, Hive Metastore, etcd, and an internal dynamic configuration system.

## Results
No specific performance numbers disclosed. The migration completed without production risk thanks to automatic fallback, and cost efficiency improved by soaking up spare Kubernetes cluster capacity with overnight batch jobs.

## Takeaways
Hide infrastructure churn behind a unified job-submission API so users never feel the Hadoop-to-K8s migration; migrate incrementally with automatic fallback rather than big-bang cutover. Running Spark on Kubernetes at scale has sharp operational edges — operator throughput, service discovery, etcd pressure — that need sharding, limits, and TTLs, and spare cluster capacity is an underused cost lever for batch workloads.
