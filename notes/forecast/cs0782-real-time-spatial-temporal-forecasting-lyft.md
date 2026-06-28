---
id: cs0782
title: Real-Time Spatial Temporal Forecasting @ Lyft
company: Lyft
primary_category: forecast
sub_category: time-series
year: 2025
source_url: https://eng.lyft.com/real-time-spatial-temporal-forecasting-lyft-fa90b3f3ec24
tags: [demand forecasting, pricing]
---

# Real-Time Spatial Temporal Forecasting @ Lyft
**Lyft** · 2025 · [source](https://eng.lyft.com/real-time-spatial-temporal-forecasting-lyft-fa90b3f3ec24)

## Problem
Lyft needs to forecast rideshare demand and supply at fine spatial-temporal granularity (geohash-6, every 5 minutes) across hundreds of North American cities to drive dynamic pricing and real-time driver incentives. The data is high-dimensional, high-frequency, and noisy, with sparse observations and intermittent local spikes from events.

## Approach / System design
A dual-model strategy:
- Time-series models (auto-regression/ARIMA, spatial-temporal covariance, dimensionality reduction via SVD/PCA) refit every minute for fast adaptation and short horizons.
- Deep neural nets (RNN/LSTM, CNN) refit a few times per day for longer horizons.

Asynchronous streaming pipelines separate training from inference, prioritizing reliability and scalability over peak accuracy. The system produces forecasts for ~4M geohashes per minute per signal.

## Key decisions
- For short horizons (5–45 min) under latency constraints, minutely-refit time-series models beat hourly-refit DNNs by better capturing near-term autocorrelation.
- Signal characteristics drive model choice: noisier demand signals favor time series; smoother supply signals work with either.
- Prefer simpler models for ~100x cheaper training, better interpretability, and easier debugging, despite DNNs' theoretical edge.
- Monitoring triggers alerts when metrics fall outside expected bounds.

## Stack
Streaming/data: Apache Beam on Apache Flink, AWS MSK, Kinesis, DynamoDB, ClickHouse, Kafka. ML infra: Lyft ML Platform, Apache Airflow, AWS SageMaker. Models: ARIMA/auto-regression, SVD/PCA, RNN/LSTM, CNN.

## Results
The article emphasizes pragmatic trade-offs over absolute accuracy: time-series gives better overall accuracy once latency is considered; supply forecasts consistently beat demand forecasts; complex terrain degrades DNNs more than time series. Scale: ~4M geohashes/minute/signal.

## Takeaways
At minute-level latency with refit constraints, simpler minutely-refit time-series models can outperform deep nets on short horizons while being far cheaper and easier to operate. Match the model to the signal's noise profile rather than defaulting to DNNs.
