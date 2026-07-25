---
id: cs1792
title: Moving Metric Detection and Alerting System at eBay
company: eBay
primary_category: anomaly
sub_category: alerting
year: 2020
source_url: https://arxiv.org/abs/2004.02360
tags: [time-series, moving-metric-detector, unsupervised, alert-precision, production]
---

# Moving Metric Detection and Alerting System at eBay
**eBay** · 2020 · [source](https://arxiv.org/abs/2004.02360)

## Problem
eBay monitors thousands of business and product-health metric time series across domain teams. It needed an automated way to surface anomalies as actionable alerts without drowning on-call engineers in false positives and alert spam.

## Approach / System design
A two-phase production system. Phase one runs the Moving Metric Detector (MMD), a distribution-agnostic anomaly detection algorithm that decomposes trend and seasonality, optimized for speed and fully unsupervised operation, to nominate candidate alerts. Phase two applies alert-retrieval logic — a point-wise ranking model combined with business rules, with feedback mechanisms — to filter the candidates down to valid, actionable notifications.

## Key decisions
- Make detection distribution-agnostic rather than assuming a particular data distribution, since real business metrics vary widely.
- Choose a decomposition method for trend/seasonality tuned for speed and unsupervised use at scale.
- Separate detection from alerting: a ranking model plus business rules gate what actually notifies humans, preventing alert fatigue.

## Stack
Not covered in the source.

## Results
The abstract reports the system dramatically improves alert precision and avoids alert spamming in production, but gives no specific precision/recall or volume-reduction numbers. The work was presented at the AAAI-20 Workshop on Cloud Intelligence.

## Takeaways
At thousands-of-metrics scale, a good detector alone is not enough — a second filtering phase mixing learned ranking with business rules is what keeps alerts precise and trusted; distribution-agnostic methods travel better across heterogeneous real-world metrics than classical decomposition assumptions.
