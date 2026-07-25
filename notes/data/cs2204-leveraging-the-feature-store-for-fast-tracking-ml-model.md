---
id: cs2204
title: Leveraging the Feature Store for Fast-Tracking ML Model Development
company: Delivery Hero
primary_category: data
sub_category: feature-store
year: 2025
source_url: https://tech.deliveryhero.com/leveraging-the-feature-store-for-fast-tracking-ml-model-development
tags: [feature-reuse, time-to-production, model-development-velocity, ML-platform, feature-discovery]
---

# Leveraging the Feature Store for Fast-Tracking ML Model Development
**Delivery Hero** · 2025 · [source](https://tech.deliveryhero.com/leveraging-the-feature-store-for-fast-tracking-ml-model-development)

## Problem
As Delivery Hero grew, feature engineering stopped scaling: data scientists kept feature code inside individual model repositories, so teams repeatedly rebuilt the same features, duplicated effort, lacked standardization, and suffered inconsistent data quality across projects.

## Approach / System design
The ML Platform team built a centralized feature store — a shared hub where teams reuse existing features and contribute new ones through peer-reviewed pull requests to a common feature repository. The architecture splits into independent offline and online halves: the offline side transforms raw data into training features in BigQuery; the online side materializes low-latency features into Redis for inference. Airflow DAGs are auto-generated from the feature repository, Feast handles registration, materialization, and Python SDK access, and features are organized by business context (vendors, customers, products).

## Key decisions
- Support both SQL (via dbt) and Python (Kubernetes-executed) transformations so data scientists can use existing skills instead of learning a new DSL.
- Decouple offline and online modules so teams can adopt the store gradually rather than all-at-once.
- Gate feature contributions behind peer-reviewed PRs to enforce standards on a shared asset.
- Bake in monitoring from the start: Great Expectations for data-quality checks and EvidentlyAI for drift detection.
- Auto-generate orchestration (Airflow DAGs) from the repo rather than having each team hand-write pipelines.

## Stack
BigQuery (offline store), Redis (online store), Feast (registry/materialization/SDK), dbt and Python for transformations, Apache Airflow orchestration, Great Expectations and EvidentlyAI monitoring, Kubernetes execution.

## Results
The post reports qualitative outcomes — increased feature reusability, standardized feature generation, less redundant development, automated pipelines, and reduced engineering effort for application teams — but no specific quantitative metrics.

## Takeaways
A centralized feature store's main payoff is organizational: reuse and standardization compound across teams. Meeting practitioners where they are (SQL and Python paths) and allowing incremental offline/online adoption lowers the migration barrier, and treating features as peer-reviewed shared code keeps quality from degrading as contributions scale.
