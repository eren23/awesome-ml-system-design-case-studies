---
id: cs1789
title: Leveling Up Customer Experience Monitoring at Twitch: The QoUX Journey
company: Twitch
primary_category: anomaly
sub_category: observability
year: 2025
source_url: https://blog.twitch.tv/en/2025/06/26/the-qoux-journey/
tags: [client-telemetry, kinesis, cloudwatch, adaptive-thresholds, mttd]
---

# Leveling Up Customer Experience Monitoring at Twitch: The QoUX Journey
**Twitch** · 2025 · [source](https://blog.twitch.tv/en/2025/06/26/the-qoux-journey/)

## Problem
Twitch's backend monitoring systems were blind to client-side degradations that users experience directly — issues such as buffering, stream quality drops, and UI failures — which meant user-facing incidents were often detected only after viewer complaints. Backend health metrics can appear normal while client experience has already degraded, creating a gap between server-side signals and real user impact.

## Approach / System design
Twitch built QoUX, a client-side experience monitoring pipeline that collects telemetry directly from viewer clients, streams it through Amazon Kinesis, and aggregates it in five-minute windows using Lambda functions. The aggregated metrics are pushed into CloudWatch, which applies ML-based anomaly detection with adaptive thresholds to identify deviations from expected user experience baselines.

## Key decisions
Using five-minute Kinesis/Lambda aggregation windows balances detection freshness with the noise reduction needed to avoid spurious alerts from bursty client events. CloudWatch's ML anomaly detection adapts thresholds automatically to time-of-day and day-of-week patterns, which is important for Twitch's highly variable viewer traffic.

## Stack
Client-side telemetry SDK, Amazon Kinesis, AWS Lambda (aggregation), Amazon CloudWatch (ML anomaly detection with adaptive thresholds).

## Results
QoUX reduced mean time to detection for user-facing issues by approximately 40% compared to relying solely on backend monitoring.

## Takeaways
Backend infrastructure health metrics are insufficient for detecting user-facing experience degradations — client-side telemetry is required to close the gap between server health and real user impact. Five-minute streaming aggregation strikes a practical balance between detection speed and signal stability. Adaptive ML-based thresholds in CloudWatch reduce the need to manually tune alert bounds for metrics that follow strong diurnal and weekly patterns.
