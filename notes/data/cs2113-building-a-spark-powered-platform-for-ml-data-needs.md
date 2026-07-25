---
id: cs2113
title: Building a Spark-Powered Platform for ML Data Needs at Snap
company: Snap
primary_category: data
sub_category: data-pipeline
year: 2024
source_url: https://eng.snap.com/prism
tags: [Apache Spark, data platform, ML data processing, Temporal, feature engineering, job orchestration]
---

# Building a Spark-Powered Platform for ML Data Needs at Snap
**Snap** · 2024 · [source](https://eng.snap.com/prism)

## Problem
Vanilla Spark infrastructure fell short for Snap's ML workflows. ML teams need iterative experimentation with repeated large-scale data regeneration, flexibility in development but stability in production, and support for diverse formats (TFRecord, Protobuf, JSON, Parquet). Spark's steep learning curve also meant ML engineers were spending time on distributed-systems mechanics instead of model work.

## Approach / System design
Prism is a unified Spark platform that abstracts infrastructure complexity behind three components: the Prism UI Console, a centralized interface consolidating previously fragmented tools (Spark UI, History Server, billing); the Prism Template, a YAML-based, config-driven framework of reusable modules for defining jobs; and the Prism Control Plane, built on Temporal, which orchestrates cluster lifecycle and job submission. Concerns are cleanly separated: the control plane owns metadata and configuration while the workflow engine handles runtime orchestration — provisioning, submission, tracking, and retries. A dedicated metrics system stores standardized signals in Spanner for time-series analysis and automation.

## Key decisions
- Adopt Temporal for reliable, scalable workflow orchestration instead of managing cluster lifecycles by hand.
- Config-driven templates to cut implementation variability across teams and lower the Spark barrier for ML engineers.
- Standardized job metrics persisted in Spanner to enable analysis and automated operations.
- Deliver a serverless-like user experience while keeping Spark's scalability underneath.

## Stack
Apache Spark on Google Dataproc, Temporal for orchestration, Spanner for metrics, Iceberg/TFRecords/BigQuery as sources and sinks, Trino for lakehouse querying, and Airflow/Kubeflow integration for scheduling.

## Results
Within two years, job volume grew from single digits per day to several thousand daily, peaking at over 10,000 Spark jobs per day.

## Takeaways
Platform leverage comes from dual adoption paths: advanced teams use Prism directly while other internal domain tools embed it. Investing in a unified interface and config-driven templates reduces friction now and creates the foundation for sustainable platform evolution later.
