---
id: cs2212
title: How Hapag-Lloyd Improved Schedule Reliability with ML-Powered Vessel Schedule Predictions Using Amazon SageMaker
company: Hapag-Lloyd
primary_category: forecast
sub_category: eta-prediction
year: 2025
source_url: https://aws.amazon.com/blogs/machine-learning/how-hapag-lloyd-improved-schedule-reliability-with-ml-powered-vessel-schedule-predictions-using-amazon-sagemaker/
tags: [xgboost, sagemaker, ais-data, mlops, vessel-eta, maritime-logistics, multi-model, step-functions]
---

# How Hapag-Lloyd Improved Schedule Reliability with ML-Powered Vessel Schedule Predictions Using Amazon SageMaker
**Hapag-Lloyd** · 2025 · [source](https://aws.amazon.com/blogs/machine-learning/how-hapag-lloyd-improved-schedule-reliability-with-ml-powered-vessel-schedule-predictions-using-amazon-sagemaker/)

## Problem
Hapag-Lloyd operates 308+ vessels over roughly 1,200 port-to-port routes with 3,500+ monthly arrivals, and schedule reliability (arriving within one calendar day of the ETA) is a key industry metric. Their legacy rule-based statistical approach couldn't handle dynamic factors like weather, port congestion, labor strikes, or routing changes, and delays cascade — a late arrival in Rotterdam ripples through Hamburg and the rest of the schedule.

## Approach / System design
A hierarchical ML system splits a voyage into modular legs, each with a specialized model: an Ocean model predicting time to the next port from real-time AIS data (position, speed, course); a Transit model forecasting port-to-port sailing times from historical performance and seasonality; and a Berth model estimating port dwell time. Predictions are combined sequentially to produce end-to-end ETAs. AIS data is ingested in 20-minute batches via Lambda (~35M observations stored), preprocessed with AWS Glue into Apache Iceberg tables on S3. Training runs on SageMaker with reusable SageMaker Pipelines, orchestrated by Step Functions to enforce the correct model dependency order, with versions tracked in the Model Registry. Serving is hybrid: nightly EventBridge-triggered batch jobs compute hierarchical predictions into RDS, while an API Gateway + Lambda real-time API handles ad-hoc schedule changes such as port omissions.

## Key decisions
- Hierarchical, modular models per journey leg rather than one monolithic network model — preserves explainability and reusability, building stakeholder trust.
- Temporal data splitting to avoid leakage: training only uses information that would have been available at prediction time.
- Hybrid batch + real-time inference: nightly batch for data-heavy preprocessing, real-time API for same-day schedule modifications, with fallback values stored in RDS.

## Stack
Amazon SageMaker (training, batch inference, Pipelines, Model Registry, Processing for hyperparameter tuning), AWS Glue, Apache Iceberg, S3, Lambda, Step Functions, EventBridge, API Gateway, Amazon RDS, Amazon SES for alerts. XGBoost-based models on AIS vessel-tracking data.

## Results
ETA MAE improved roughly 12% over the legacy system; API responses in the hundreds of milliseconds, more than 80% faster than the prior solution; 99.5% availability target. Hapag-Lloyd climbed two positions in international schedule reliability rankings, covering 120 vessel services across ~1,200 routes.

## Takeaways
Modular, explainable model decomposition eases business adoption compared to black-box ML. Standardized MLOps (pipeline blueprints, model registry, orchestrated training) enables fast, governed iteration at fleet scale. Strict temporal handling of training data and a freshness/cost balance (20-minute AIS batches plus nightly retraining) were central to making predictions trustworthy in a domain where delays cascade through the whole network.
