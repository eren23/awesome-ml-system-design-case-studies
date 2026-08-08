---
id: cs1856
title: Airbnb — How Airbnb Standardized Metric Computation at Scale
company: Airbnb
primary_category: data
sub_category: data-pipeline
year: 2021
source_url: https://medium.com/airbnb-engineering/how-airbnb-standardized-metric-computation-at-scale-9afe6695b486
tags: [metrics, minerva, declarative, backfill, computation, data-pipeline]
---

# Airbnb — How Airbnb Standardized Metric Computation at Scale
**Airbnb** · 2021 · [source](https://medium.com/airbnb-engineering/how-airbnb-standardized-metric-computation-at-scale-9afe6695b486)

## Problem
Even after Minerva established a single source of truth for metric definitions, computing those metrics consistently across multiple consumption contexts — dashboards, experiments, ad-hoc queries — remained an engineering challenge. Teams had built parallel computation paths that produced divergent results or required redundant infrastructure, and backfilling historical values when definitions changed was manual and error-prone.

## Approach / System design
Minerva's computation layer allows metric authors to write declarative definitions that specify what to compute, not how. The platform's compute engine translates these definitions into physical jobs automatically. When a definition changes or a new metric is added, Minerva automatically schedules backfill jobs to recompute historical data without manual intervention. Dataset replacement is designed to be zero-downtime, so downstream consumers see no interruption during recomputation.

## Key decisions
Adopting a declarative model for metric computation separates the concern of business logic from execution strategy, allowing the platform to optimize or re-platform the underlying compute without requiring metric authors to change their definitions. Automatic backfilling was prioritized because manual backfills were a significant source of errors and inconsistency in the previous system.

## Stack
Minerva computation framework, declarative metric definition layer, automated backfill orchestration, internal data pipeline infrastructure.

## Results
Not covered in the source.

## Takeaways
Standardizing computation alongside definition — not just specifying what a metric means but enforcing how it is always computed — is what ultimately eliminates metric divergence in practice. Declarative definitions combined with automated backfills reduce both operational burden and the risk of historical inconsistencies when business logic evolves.
