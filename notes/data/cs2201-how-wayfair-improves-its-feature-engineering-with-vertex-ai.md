---
id: cs2201
title: How Wayfair Improves Its Feature Engineering with Vertex AI
company: Wayfair
primary_category: data
sub_category: feature-store
year: 2024
source_url: https://cloud.google.com/blog/products/ai-machine-learning/how-wayfair-improves-its-feature-engineering-with-vertex-ai
tags: [vertex-ai, bigquery, training-serving-skew, centralized-features, github-governance, feature-pipelines, google-cloud]
---

# How Wayfair Improves Its Feature Engineering with Vertex AI
**Wayfair** · 2024 · [source](https://cloud.google.com/blog/products/ai-machine-learning/how-wayfair-improves-its-feature-engineering-with-vertex-ai)

## Problem
Wayfair's ad hoc feature engineering left multiple versions of the same feature scattered across models, making sharing hard; there was minimal oversight of feature freshness, schemas, or data guarantees; training-serving skew caused models to behave differently in production than in development; and feature curation plus new model development took several months per iteration.

## Approach / System design
Wayfair centralized feature engineering on Google Cloud. Raw data lands in BigQuery; a centralized repository of feature definitions lives in GitHub, where changes go through a PR-approval process for governance and traceability. Vertex AI Pipelines execute SQL to extract, transform, and ingest data into Vertex AI Feature Store, which serves both point-in-time lookups for training and low-latency online serving for inference — the same feature values in both paths. Pipelines are triggered on static schedules by Cloud Scheduler or dynamically by other pipelines, with Cloud Functions listening to Pub/Sub messages to kick off runs.

## Key decisions
- Adopted a managed feature store specifically to guarantee offline-online consistency and kill training-serving skew, rather than patching skew case-by-case.
- Put feature definitions under GitHub PR governance, so features are reviewed, versioned, and auditable like code.
- Supported multi-cadence pipelines — both scheduled and dynamically triggered — via Pub/Sub + Cloud Scheduler + Cloud Functions.
- Planned migration to the BigQuery-powered Vertex AI Feature Store version (then in public preview) to reduce cloud costs.

## Stack
Vertex AI Feature Store, Vertex AI Pipelines, BigQuery, Cloud Functions, Pub/Sub, Cloud Scheduler, GitHub (governance/version control).

## Results
No specific quantitative post-implementation metrics are reported. Qualitatively: consistent features between development and production, confident iteration without data-related surprises, easy sharing and reuse, and guaranteed feature freshness.

## Takeaways
Training-serving skew is best eliminated architecturally — one governed store serving both training and inference — rather than by per-model fixes. Treating feature definitions as code under PR review brings ML data the same governance discipline as software, and managed cloud components (pipelines, pub/sub triggers, scheduler) let a small team run multi-cadence feature pipelines without bespoke orchestration.
