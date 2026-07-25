---
id: cs1802
title: Finding Anomalies in User Behavior with Python
company: Indeed
primary_category: anomaly
sub_category: alerting
year: 2016
source_url: https://engineering.indeedblog.com/blog/2016/10/finding-anomalies-with-python/
tags: [s-h-esd, stl-decomposition, time-series, alerting, python]
---

# Finding Anomalies in User Behavior with Python
**Indeed** · 2016 · [source](https://engineering.indeedblog.com/blog/2016/10/finding-anomalies-with-python/)

## Problem
Indeed serves over 200 million unique visitors a month, and its metrics swing legitimately with day of week, time of day, and holidays. Simple outlier detection couldn't separate real system failures from these expected fluctuations, so meaningful anomalies in pageview and server metrics went undetected or drowned in noise.

## Approach / System design
The team adopted Twitter's Seasonal-Hybrid-ESD statistical anomaly detection methodology and ported it from R to Python. Historical data establishes a baseline of expected behavior — seasonality and trend are removed via Seasonal and Trend decomposition using LOESS (STL) — and actual metrics are compared against those expectations, flagging significant deviations instead of applying fixed thresholds. The Python port plugs into Indeed's existing internal alerting systems.

## Key decisions
- Build on Twitter's AnomalyDetection library, which improves on the classic Grubbs test by using the median — more precise for web-traffic data than mean-based variants.
- Port to Python rather than run the original R library, so the detector integrates with Indeed's Python-based internal alerting.
- Lean on existing open-source math libraries (pyloess, NumPy, SciPy) instead of reimplementing the underlying routines.
- Publish the resulting port as open source on GitHub.

## Stack
Python, STL decomposition (via pyloess), NumPy, SciPy; open-source port of Twitter's AnomalyDetection.

## Results
One developer completed the port in roughly a week by reusing existing mathematical libraries, giving Indeed seasonal-aware anomaly detection over metrics for its 200M+ monthly visitors.

## Takeaways
Seasonality-aware, median-based detection (S-H-ESD over STL residuals) is what makes anomaly detection usable on web-traffic metrics — and standing on community-built implementations turns a research-grade method into a production alerting feed in about a week of one engineer's time.
