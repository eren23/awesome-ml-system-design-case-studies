---
id: cs1791
title: How We Detect Anomalies in Our Product Recommendations Metrics
company: Wayfair
primary_category: anomaly
sub_category: alerting
year: 2019
source_url: https://www.aboutwayfair.com/tech-innovation/how-we-detect-anomalies-in-our-product-recommendations-metrics
tags: [recommendations, kpi-monitoring, airflow, statistical, alerting]
---

# How We Detect Anomalies in Our Product Recommendations Metrics
**Wayfair** · 2019 · [source](https://www.aboutwayfair.com/tech-innovation/how-we-detect-anomalies-in-our-product-recommendations-metrics)

## Problem
Wayfair's product recommendations system generates high-volume throughput metrics that must be monitored continuously to catch degradations before they affect customer experience. Naive statistical alerting on these metrics produced approximately 8 false-positive alerts per week, causing alert fatigue and slowing the team's ability to respond to genuine production issues.

## Approach / System design
Wayfair built an in-house anomaly detector orchestrated by Apache Airflow that computes rolling mean and standard deviation over recent metric history and flags points that fall outside a 95% confidence band. To reduce false positives, alerts only fire if at least three consecutive data points are flagged as anomalous, requiring a sustained deviation rather than a single-point outlier to trigger a notification.

## Key decisions
Requiring three consecutive anomalous observations before alerting is the primary noise-reduction mechanism; a single-point outlier common in recommendation throughput data no longer triggers a page. Using Airflow for orchestration integrates anomaly detection naturally into the existing data pipeline workflow and provides scheduling, dependency management, and visibility without building bespoke infrastructure.

## Stack
Apache Airflow (orchestration), Python (statistical detection using mean/std confidence bands), internal metrics pipeline.

## Results
The system reduced false-positive alerts from approximately 8 per week to near zero, and it caught a genuine production degradation in the recommendations system that would otherwise have gone undetected.

## Takeaways
Requiring consecutive anomalies rather than single-point detections is a simple and highly effective technique for reducing alert fatigue in systems with inherently bursty metrics. Standard statistical methods (mean ± 2σ) are often sufficient for KPI monitoring when combined with appropriate noise filtering. Integrating anomaly detection into an existing workflow orchestration tool like Airflow reduces the infrastructure overhead of building a standalone monitoring service.
