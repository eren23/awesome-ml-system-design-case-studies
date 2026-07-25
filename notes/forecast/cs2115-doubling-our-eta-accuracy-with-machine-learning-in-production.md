---
id: cs2115
title: Doubling Our ETA Accuracy with Machine Learning in Production
company: Transporeon
primary_category: forecast
sub_category: eta-prediction
year: 2024
source_url: https://transporeon-visibility-hub.medium.com/doubling-our-eta-accuracy-with-machine-learning-in-production-15e8dff5bc4e
tags: [eta-prediction, road-freight, logistics, heuristics-to-ml, production, route-learning]
---

# Doubling Our ETA Accuracy with Machine Learning in Production
**Transporeon** · 2024 · [source](https://transporeon-visibility-hub.medium.com/doubling-our-eta-accuracy-with-machine-learning-in-production-15e8dff5bc4e)

## Problem
Sixfold (Transporeon's visibility platform) needed ETAs for millions of road-freight shipments across Europe. Navigation-style optimal-route calculations don't work for trucks: drivers take mandated breaks, follow driving-time regulations, and deviate from standard routes, so rule-based heuristics were unreliable — especially at long horizons.

## Approach / System design
The team trained an ML model on historical GPS telemetry (from thousands of fleet management providers, of variable quality) joined with shippers' transport plans, so the model learns real-world driver behavior — individual route preferences, break patterns, likely delays. The data pipeline lands data in BigQuery, with Cloud Composer (Airflow) running data-quality checks; feature calculations happen on-the-fly in BigQuery rather than through a cached feature store. The model retrains weekly via a Kubeflow pipeline, is automatically tested against the live model as a baseline, and ships only after a manual GitHub pull-request approval. Pre- and post-processing (encoding, outlier handling, heuristic rules) live in scikit-learn pipelines bundled with the model.

## Key decisions
- Learn driver behavior from telemetry instead of computing idealized routes.
- BigQuery as the warehouse, chosen for its geographical functions and Google-ecosystem integration; on-the-fly feature computation instead of a feature store.
- Weekly automated retraining with champion/challenger testing plus a human approval gate.
- Package preprocessing, model, and postprocessing into a single scikit-learn pipeline artifact — separating them had caused maintenance and train/serve consistency bugs.

## Stack
BigQuery, PostgreSQL (Cloud SQL), Google Cloud Composer (Airflow), Kubeflow Pipelines, scikit-learn, Parquet on Cloud Storage, Grafana for monitoring.

## Results
Prediction error for long-horizon estimates (4+ hours out) was nearly halved versus the heuristic approach. The model ran over a year in production without major changes despite 10x growth in data volume.

## Takeaways
Research notebooks rarely survive contact with production — expect a full rewrite. Subtle database implementation differences (spatial functions, date math) introduce train/serve inconsistencies, and shipping all model logic as one deployable artifact is the reliable way to prevent environment-specific bugs.
