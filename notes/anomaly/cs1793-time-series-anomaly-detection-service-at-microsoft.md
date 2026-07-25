---
id: cs1793
title: Time-Series Anomaly Detection Service at Microsoft
company: Microsoft
primary_category: anomaly
sub_category: observability
year: 2019
source_url: https://arxiv.org/abs/1906.03821
tags: [spectral-residual, cnn, azure, unsupervised, at-scale]
---

# Time-Series Anomaly Detection Service at Microsoft
**Microsoft** · 2019 · [source](https://arxiv.org/abs/1906.03821)

## Problem
Large enterprises need continuous, real-time monitoring of business and application metrics (page views, revenue, and the like) to catch incidents promptly. Microsoft needed an anomaly-detection service accurate and efficient enough to monitor huge numbers of time series continuously, without labeled training data.

## Approach / System design
The production service is organized into three modules: data ingestion, an experimentation platform, and online compute. Its core detector is a novel algorithm combining Spectral Residual (SR) — a technique borrowed from visual saliency detection — with a Convolutional Neural Network (CNN). This is the first application of SR to time-series anomaly detection; SR transforms the series into a saliency map on which the CNN discriminates anomalies.

## Key decisions
- Design around three pillars: accuracy, efficiency, and generality, since the service must work unsupervised across arbitrary customer metrics.
- Transfer a visual-saliency technique (SR) across domains to time series, then stack a CNN on the saliency output rather than on raw values.
- Build the platform as separable ingestion, experimentation, and online-compute modules so algorithms can be evaluated and served independently.

## Stack
Spectral Residual + CNN detector; runs as a Microsoft/Azure production service. Specific infrastructure is not detailed in the abstract.

## Results
The paper (accepted at KDD 2019) reports superior accuracy versus state-of-the-art baselines on both public datasets and Microsoft production data; specific figures are not in the abstract. The service monitors millions of time series per minute in production.

## Takeaways
Cross-domain technique transfer can unlock gains — treating a time series as a saliency-detection problem made an unsupervised detector both accurate and general — and packaging it with ingestion and experimentation infrastructure is what turns an algorithm into a service monitoring millions of series per minute.
