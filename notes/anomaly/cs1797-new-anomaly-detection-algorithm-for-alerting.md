---
id: cs1797
title: New Anomaly Detection Algorithm for Alerting
company: Cisco ThousandEyes
primary_category: anomaly
sub_category: alerting
year: 2024
source_url: https://medium.com/thousandeyes-engineering/new-anomaly-detection-algorithm-for-alerting-e1709ab11832
tags: [tukey-fences, flink, percentiles, dynamic-baselining, false-positives]
---

# New Anomaly Detection Algorithm for Alerting
**Cisco ThousandEyes** · 2024 · [source](https://medium.com/thousandeyes-engineering/new-anomaly-detection-algorithm-for-alerting-e1709ab11832)

## Problem
ThousandEyes' dynamic baselining for alert rules used a standard-deviation method that implicitly assumes Gaussian-distributed metrics. Real network metrics frequently violate that assumption, producing excessive false-positive alerts.

## Approach / System design
The team evaluated three candidate detectors — standard-deviation-based, percentile-based, and Tukey Fences — and chose Tukey Fences, which builds its fences from percentiles instead of mean and standard deviation and therefore calibrates well across non-Gaussian distributions. Sensitivity is exposed as low/medium/high levels controlled by a single k parameter. The production implementation runs on Apache Flink, computing percentiles over 5-minute windows and caching them for lookup by the alerting engine.

## Key decisions
- Move from distribution-dependent (mean/std) to distribution-agnostic (percentile-based) baselining.
- Encode customer-facing sensitivity as one tunable k parameter mapped to three named levels.
- Stream-compute percentiles in Flink on a 5-minute cadence with a caching layer, so alert evaluation stays a cheap lookup.
- Validate with a custom scoring methodology on three major customers' most-used metrics before rollout.

## Stack
Apache Flink for stream processing, plus a caching layer for computed percentile values.

## Results
Calibration error improved about 60% (the SD method deviated 15% from ideal vs. 6% for Tukey). Anomaly separation improved 16% (effect size 0.73 to 0.85). Alert accuracy improved 15% at medium sensitivity and up to 33% at low sensitivity, with reduced false positives.

## Takeaways
When production metrics are heterogeneous and non-Gaussian, distribution-agnostic detectors beat parametric ones; and packaging the detector's tuning surface as a single sensitivity knob keeps customization usable without sacrificing detection quality.
