---
id: cs1801
title: How Agoda Enhanced the Uptime and Consistency of Financial Metrics
company: Agoda
primary_category: anomaly
sub_category: outlier-detection
year: 2025
source_url: https://medium.com/agoda-engineering/how-agoda-enhanced-the-uptime-and-consistency-of-financial-metrics-ef7d54c4e4f0
tags: [data-quality, financial-metrics, spark, ml-monitoring, data-contracts]
---

# How Agoda Enhanced the Uptime and Consistency of Financial Metrics
**Agoda** · 2025 · [source](https://medium.com/agoda-engineering/how-agoda-enhanced-the-uptime-and-consistency-of-financial-metrics-ef7d54c4e4f0)

## Problem
Multiple Agoda teams independently ran their own financial data pipelines, producing duplicate sources, redundant processing, and inconsistent metric definitions and transformations. The differences in data handling led to inconsistent reporting and operational delays, and there was no centralized monitoring to catch quality problems.

## Approach / System design
Agoda consolidated everything into FINUDP, the Financial Unified Data Pipeline, a centralized Apache Spark pipeline built around three non-functional pillars: freshness (hourly updates, monitored by an internal "GoFresh" tool that flags delays), reliability (automated data-quality checks validating every column against predefined rules, with the pipeline pausing on critical rule violations), and maintainability (mandatory peer reviews, shadow testing in a non-prod environment, and a 90% unit-test coverage target). On top of the rule-based validations, ML-based anomaly detection models watch the millions of daily financial data points for unusual fluctuations, and a three-tier alerting setup (email, Slack, NOC) routes failures.

## Key decisions
- Establish formal data contracts with upstream teams so bad data is stopped at ingestion rather than cleaned downstream.
- Shadow-test changes in a non-production environment before deploying to production.
- Pause the pipeline on critical validation failures to prevent incorrect data from propagating.
- Layer ML anomaly detection over deterministic column-level rules rather than relying on either alone.

## Stack
Apache Spark, GoFresh (internal freshness monitoring), Quilliup (third-party data-quality/integrity testing), ML anomaly-detection models, Slack/email/NOC alerting.

## Results
Pipeline runtime dropped from 5 hours to roughly 30 minutes (about an 83% improvement). Uptime reached 95.6% against a 99.5% target, across millions of daily financial data points.

## Takeaways
For financial data, centralization is a deliberate trade of team velocity for reliability and governance — and it only works with shared metric definitions, formal upstream contracts, and multi-layered monitoring (freshness, rule-based quality, integrity, and ML anomaly detection) stacked together.
