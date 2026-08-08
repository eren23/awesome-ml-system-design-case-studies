---
id: cs1849
title: LinkedIn — Towards Data Quality Management at LinkedIn
company: LinkedIn
primary_category: data
sub_category: data-quality
year: 2022
source_url: https://www.linkedin.com/blog/engineering/data-management/towards-data-quality-management-at-linkedin
tags: [data-quality, data-health-monitor, metadata, freshness, completeness, alerting]
---

# LinkedIn — Towards Data Quality Management at LinkedIn
**LinkedIn** · 2022 · [source](https://www.linkedin.com/blog/engineering/data-management/towards-data-quality-management-at-linkedin)

## Problem
LinkedIn operates tens of thousands of datasets that underpin product features, analytics, and machine learning models. Without systematic monitoring, data issues — stale partitions, missing records, unexpected schema changes — go undetected until they surface as downstream product bugs or incorrect model predictions. Scaling a manual or rule-based monitoring approach to cover the full catalog is not viable.

## Approach / System design
LinkedIn built the Data Health Monitor (DHM), a metadata-driven observability system structured around three layers: observe, understand, and reason. The observe layer collects metadata signals (partition freshness, record counts, schema snapshots) continuously across datasets. The understand layer interprets these signals by comparing them against learned baselines and declared SLAs. The reason layer triggers alerts and root-cause analysis workflows when anomalies are detected across four quality dimensions: availability, freshness, completeness, and schema consistency.

## Key decisions
Driving the system from metadata rather than scanning the underlying data keeps the monitoring overhead low and avoids data-size-dependent compute costs. Organizing the architecture into observe/understand/reason layers separates data collection from analysis and alerting, making each component independently evolvable. Focusing on four well-defined quality dimensions gives dataset owners actionable categories for remediation rather than a generic "something is wrong" signal.

## Stack
Data Health Monitor (DHM), metadata collection infrastructure, internal alerting and on-call tooling, LinkedIn's data platform.

## Results
DHM monitors approximately 150,000 critical datasets and achieves above 98% alert accuracy.

## Takeaways
Metadata-driven monitoring is the right abstraction for scaling data quality observability to very large dataset catalogs because it avoids the cost of full data scans. High alert accuracy (above 98%) requires careful baseline modeling and anomaly detection tuning; false positives erode trust in the monitoring system and cause alert fatigue just as missed issues do.
