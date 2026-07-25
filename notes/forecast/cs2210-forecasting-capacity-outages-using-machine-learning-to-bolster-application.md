---
id: cs2210
title: Forecasting Capacity Outages Using Machine Learning to Bolster Application Resiliency
company: Goldman Sachs
primary_category: forecast
sub_category: capacity
year: 2024
source_url: https://developer.gs.com/blog/posts/forecasting-capacity-outages-using-machine-learning-to-bolster-application-resiliency
tags: [capacity-planning, change-point-detection, anomaly-detection, private-cloud, infrastructure, patent-pending, resiliency]
---

# Forecasting Capacity Outages Using Machine Learning to Bolster Application Resiliency
**Goldman Sachs** · 2024 · [source](https://developer.gs.com/blog/posts/forecasting-capacity-outages-using-machine-learning-to-bolster-application-resiliency)

## Problem
Goldman Sachs runs a global private cloud whose components — hosts, storage, network links, databases, message queues, caches, load balancers — all have finite capacity, and exhaustion threatens application resilience. Provisioning extra capacity takes time, so it can't be done reactively at the moment of exhaustion; the approach must be proactive. It also has to be accurate enough not to spam owners with alerts or drive costly over-provisioning, while still catching every genuine exhaustion risk in noisy utilization data.

## Approach / System design
The team framed it as time series forecasting: given past utilization (e.g., database space usage), predict when it will hit 100% so owners can archive data or add capacity in time. Data exploration identified three fundamental patterns — trend (continuous growth/decline), change points (sudden shifts over short spans), and seasonality (periodic patterns) — with any real series being a combination. The pipeline decomposes accordingly: (1) extract the seasonal component via Seasonal-Trend Decomposition and Periodogram Estimation, splitting the series into a repeating part and a leftover; (2) run a proprietary, patent-pending change point detection algorithm (a modification of CUSUM that works in the presence of an underlying trend) on the leftover; (3) fit the trend with ridge regression — polynomial regression for non-linear trends — using only data after the latest change point, since pre-change behavior is no longer representative. Forecasts are the sum of the extrapolated seasonal and trend components. The same forecasts power real-time anomaly detection: if current utilization deviates significantly from the forecast, the system raises an alert so owners can mitigate a surge while longer-term fixes are planned.

## Key decisions
- Decompose before modeling: stripping seasonality and isolating change points reduces the problem to well-studied cases that standard techniques handle out-of-the-box.
- Build a custom trend-robust CUSUM variant (patented) rather than using stock change point detectors.
- Fit trends only on post-change-point data, treating change points as regime boundaries.
- Reuse the forecasting model for anomaly detection by comparing actuals against predictions, instead of maintaining a separate anomaly system.
- Validate through extensive backtesting across many infrastructure component types before productionizing.

## Stack
Seasonal-Trend Decomposition, Periodogram Estimation, modified CUSUM change point detection (patent-pending), ridge and polynomial regression for trend fitting, running across Goldman's global private-cloud telemetry.

## Results
No quantitative accuracy or alert-volume metrics are published. The system underpins an extensively used internal platform for capacity planning and time series anomaly detection; the team stated plans to open-source the library and continue improving the models.

## Takeaways
Classical decomposition plus simple regressors, applied carefully, handles industrial capacity forecasting without deep models — the hard engineering is in robust change point detection amid trends and noise. Treating change points as boundaries that invalidate older data keeps forecasts honest after regime shifts, and a good forecaster doubles as an anomaly detector for free.
