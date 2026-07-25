---
id: cs2399
title: Model health assurance at LinkedIn
company: LinkedIn
primary_category: mlops
sub_category: monitoring-infra
year: 2021
source_url: https://engineering.linkedin.com/blog/2021/model-health-assurance-at-linkedin
tags: [model monitoring, model health, production ml, model reliability, data drift, performance degradation]
---

# Model health assurance at LinkedIn
**LinkedIn** · 2021 · [source](https://engineering.linkedin.com/blog/2021/model-health-assurance-at-linkedin)

## Problem
With hundreds of models centralized on the Pro-ML platform, LinkedIn had no standardized way to monitor model health: production data drifting from training data, upstream pipeline errors corrupting model inputs, training/inference code-path mismatches, and system-level issues (latency, throughput) were each handled by ad hoc, per-team custom solutions.

## Approach / System design
The health assurance (HA) layer platformizes monitoring across two lifecycle phases:
- **Offline (training)**: monitor pipeline execution metadata and model artifacts.
- **Online (inference)**: real-time monitoring of system metrics, feature distributions, and data drift.
Drift monitoring runs in two complementary modes — offline daily statistics pushed into Pinot and alerted on via ThirdEye, and real-time quantile tracking (mean, 50th/75th/90th/99th percentiles) aggregated with Samza. HA plugs into LinkedIn's existing observability estate (inGraph, TSDS) rather than inventing new dashboards.

## Key decisions
- A metric aggregation library to kill "metric bloat": host-level feature distributions are aggregated to the model level, avoiding an explosion of ~25 million potential metric keys.
- Two-track drift detection (daily offline stats + streaming quantiles) instead of a single mechanism.
- Configuration-driven onboarding: latency monitoring is auto-configured; feature tracking is declared by engineers in their training pipelines.
- "Dark canary" testing before production to catch train/serve distribution mismatches early.

## Stack
Kafka and Samza (streaming aggregation), Pinot (analytics storage), ThirdEye (anomaly detection/alerting), inGraph and TSDS (real-time and time-series monitoring), all layered on the Pro-ML platform.

## Results
HA had already surfaced major issues in production models — e.g., teams detecting zero-valued features and unexpectedly large feature values. Aggregate impact metrics are not disclosed.

## Takeaways
- Centralizing model monitoring removes duplicated per-team engineering and makes health checks a platform default.
- At 1,000+ model scale, metric aggregation is not optional — naive per-host, per-feature metrics are cardinality bombs.
- Real-time feature-distribution visibility doubles as a root-cause-analysis tool during experimentation, not just an alarm system.
