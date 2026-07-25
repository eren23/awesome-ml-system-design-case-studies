---
id: cs2383
title: Coop reduces food waste by forecasting with Google's AI and Data Cloud
company: Coop
primary_category: forecast
sub_category: eta-prediction
year: 2023
source_url: https://cloud.google.com/blog/products/ai-machine-learning/coop-reduces-food-waste-with-google-cloud-ai-and-data-cloud
tags: [vertex-ai, demand-forecasting, food-waste, inventory, automl, bigquery, fresh-produce, demand forecasting, inventory optimization, food waste, retail, Vertex AI, temporal fusion transformer, XGBoost]
---

# Coop reduces food waste by forecasting with Google's AI and Data Cloud
**Coop** · 2023 · [source](https://cloud.google.com/blog/products/ai-machine-learning/coop-reduces-food-waste-with-google-cloud-ai-and-data-cloud)

## Problem
Swiss retailer Coop needed better demand forecasts for fresh produce to optimize stock across distribution centers — over-ordering creates food waste, under-ordering hurts availability. Its existing on-premises ML setup (a single workstation running PyTorch/TensorFlow models) could not scale for fine-tuning and operationalizing models.

## Approach / System design
Data flows from SAP systems into BigQuery; data scientists work in Vertex AI Workbench; Vertex AI Forecast (AutoML) trains the demand forecasting models; predictions stream back into SAP for order management. Rollout went through a pilot at one distribution center before expanding to all Swiss distribution centers. Coop also built a broader internal ML platform on GKE and Vertex AI to standardize how teams work.

## Key decisions
- Chose Vertex AI Forecast (AutoML) over continuing with custom in-house models — it was benchmarked against their own XGBoost and Temporal Fusion Transformer (PyTorch) models.
- Migrated from on-prem to Google Cloud so infrastructure stopped being the bottleneck.
- Kept SAP as the system of record, integrating forecasts back into existing order-management workflows.
- Used quantile inference to handle forecast uncertainty for ordering decisions.

## Stack
BigQuery (data warehouse), Vertex AI Workbench (development), Vertex AI Forecast (AutoML training), GKE (platform orchestration), SAP (data source and order management), PyTorch/TensorFlow (legacy baseline models).

## Results
- 14.5 WAPE (weighted average percentage error) on fresh-produce demand forecasts.
- 43% performance improvement over the custom models previously run on their own VMs (XGBoost and Temporal Fusion Transformer).
- More precise ordering, less excess inventory/food waste, and better product availability, supporting Coop's sustainability goals.

## Takeaways
- AutoML forecasting beat carefully built custom gradient-boosting and deep-learning baselines by a wide margin with far less operational complexity.
- Tight BigQuery–Vertex AI integration and a pilot-then-scale rollout de-risked the migration.
- Quantile forecasts (not just point estimates) are what make demand predictions actionable for inventory control.
