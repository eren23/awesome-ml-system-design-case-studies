---
id: cs1795
title: Real-world Insights: Anomaly Detection in Internet Traffic
company: trivago
primary_category: anomaly
sub_category: alerting
year: 2024
source_url: https://tech.trivago.com/post/2024-02-13-real-world-insights-anomaly-detection-in-internet-traffic
tags: [prophet, arima, traffic, forecasting, partner-monitoring]
---

# Real-world Insights: Anomaly Detection in Internet Traffic
**trivago** · 2024 · [source](https://tech.trivago.com/post/2024-02-13-real-world-insights-anomaly-detection-in-internet-traffic)

## Problem
trivago sends traffic to hundreds of partner hotel booking sites and needs to monitor that traffic to detect partner data outages and unexplained volume changes quickly. Manual monitoring at this scale is infeasible, and naive threshold alerts generate excessive false positives because internet traffic has strong weekly and seasonal patterns that must be accounted for.

## Approach / System design
trivago trains time-series forecasting models per partner site and raises alerts when observed traffic deviates beyond the model's confidence interval. Prophet is deployed in production as the primary forecasting engine because it handles multiple seasonality patterns and missing data robustly; ARIMA variants were evaluated as alternatives. Alerts only fire when traffic deviates consistently beyond confidence bounds, reducing noise from transient fluctuations.

## Key decisions
Choosing confidence-interval deviation alerting rather than static thresholds accounts for the varying traffic scale across partners and for natural seasonal variation. Prophet's built-in handling of holidays and multiple seasonality periods made it more robust than ARIMA for the weekly and daily traffic cycles typical of hotel search.

## Stack
Prophet (production forecasting), ARIMA (evaluated alternative), Python-based monitoring pipeline.

## Results
Not covered in the source.

## Takeaways
Forecasting-based anomaly detection outperforms static thresholds for traffic monitoring because it naturally adapts to weekly and seasonal patterns. Prophet's flexibility with multiple seasonality and its ability to handle gaps in training data make it well-suited for monitoring diverse partner sites with different traffic profiles. Confidence-interval deviation alerts provide a principled mechanism for distinguishing genuine anomalies from expected variation.
