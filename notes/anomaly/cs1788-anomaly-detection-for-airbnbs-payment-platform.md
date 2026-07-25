---
id: cs1788
title: Anomaly Detection for Airbnb's Payment Platform
company: Airbnb
primary_category: anomaly
sub_category: outlier-detection
year: 2015
source_url: https://medium.com/airbnb-engineering/anomaly-detection-for-airbnb-s-payment-platform-e3b0ec513199
tags: [time-series, payments, FFT, seasonality, monitoring]
---

# Anomaly Detection for Airbnb's Payment Platform
**Airbnb** · 2015 · [source](https://medium.com/airbnb-engineering/anomaly-detection-for-airbnb-s-payment-platform-e3b0ec513199)

## Problem
Airbnb's payments platform spans 190 countries with many currencies and payment processors, and things break unpredictably — a currency suddenly can't be processed, or a payment gateway goes offline. The team needed to detect such operational failures in near real time across many data dimensions without manual watching.

## Approach / System design
Payment time series are decomposed into three components — Y = Seasonality + Trend + Error — and each is modeled separately. Seasonality is discovered automatically with a Fast Fourier Transform rather than assumed (e.g., one product category showed peaks at 7- and 3.5-day periods, another weekly plus 40-day cycles). Trend is captured with a rolling 14-day median, chosen over the mean for robustness against outliers. What remains is the error term; an alert fires when the error exceeds 4 standard deviations from zero.

## Key decisions
- Replace the earlier OLS-regression approach — which hard-coded weekly seasonality and linear growth — with FFT-detected seasonality so the model generalizes across metrics.
- Use a rolling median rather than a mean for trend, resisting distortion from sudden spikes.
- Keep assumptions minimal so the same detector scales across diverse payment datasets beyond the original use case.

## Stack
FFT-based spectral analysis plus statistical modeling (rolling median trend, standard-deviation thresholding). No specific frameworks are named.

## Results
The article reports the model performs well at identifying anomalies while making minimal assumptions, but publishes no precision/recall or false-positive figures.

## Takeaways
The fewer assumptions an anomaly detector encodes — letting the data reveal its own seasonality and using robust statistics for trend — the more broadly it applies across an organization's heterogeneous metrics.
