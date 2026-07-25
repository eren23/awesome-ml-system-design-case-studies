---
id: cs2260
title: 500X Scalability of Experiment Metric Computing with Unified Dynamic Framework
company: Pinterest
primary_category: mlops
sub_category: experimentation
year: 2025
source_url: https://medium.com/pinterest-engineering/500x-scalability-of-experiment-metric-computing-with-unified-dynamic-framework-9eb356fee676
tags: [experimentation, apache-airflow, dynamic-dag, a/b-testing, metrics, scalability, pipeline-automation]
---

# 500X Scalability of Experiment Metric Computing with Unified Dynamic Framework
**Pinterest** · 2025 · [source](https://medium.com/pinterest-engineering/500x-scalability-of-experiment-metric-computing-with-unified-dynamic-framework-9eb356fee676)

## Problem
Pinterest's experimentation platform computed 1,500+ user-defined daily metrics, and the pipeline depended on users' custom upstream data-insertion jobs: a delay in one upstream job could stall the entire pipeline. Skipped metrics were hard to backfill and track, and the system hit frequent out-of-memory errors, capping scalability.

## Approach / System design
The Unified Dynamic Framework (UDF) uses a two-layer design:
- **Metric computing layer**: encapsulates logic for different metric types (aggregated, calendar-day, user-defined functions).
- **Dynamic DAG creation layer**: generates Airflow pipeline structures based on data readiness, so metrics are processed in parallel batches on a first-come, first-served basis — ready inputs are prioritized immediately instead of waiting for all upstream jobs.

A persistence mechanism tracks in-flight metrics to prevent duplicate computation; automatic backfilling detects and reprocesses skipped metrics within a configurable N-day window; and a centralized Experiment Metrics Metadata system serves as the single source of truth for metric definitions.

## Key decisions
- Use Airflow Dynamic DAGs keyed on data readiness rather than static DAGs blocked on the slowest upstream dependency.
- Build duplicate-prevention state so adaptive batching can't double-compute metrics.
- Make backfill automatic and windowed instead of manual and ad hoc.
- Centralize metric metadata to enable self-serve metric creation on top of shared infrastructure.

## Stack
Apache Airflow (dynamic DAG generation), Spark (computation engine for custom functions), Druid (metric storage and visualization), Helium (Pinterest's internal experimentation platform).

## Results
- Supports 100x current metric volume, with a design target of 500x.
- Metrics delivered 4x faster, measured from source-data-ready to final results.
- ~90% of partial-data issues resolved by automatic backfills; maintenance work from upstream failures eliminated.
- New metric pipeline creation reduced from months to days.

## Takeaways
Decoupling metric computation from rigid pipeline topology — letting the DAG adapt to what data is actually ready — removes the "slowest upstream stalls everything" failure mode. Standardizing on a unified framework converts a bespoke-pipeline maintenance burden into self-serve metric creation, which is where the developer-velocity gain comes from.
