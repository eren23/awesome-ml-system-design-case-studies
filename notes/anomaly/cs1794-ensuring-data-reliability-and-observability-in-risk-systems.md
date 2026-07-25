---
id: cs1794
title: Ensuring Data Reliability and Observability in Risk Systems
company: Grab
primary_category: anomaly
sub_category: alerting
year: 2024
source_url: https://engineering.grab.com/data-observability
tags: [data-quality, flink, datadog, streaming, alerting]
---

# Ensuring Data Reliability and Observability in Risk Systems
**Grab** · 2024 · [source](https://engineering.grab.com/data-observability)

## Problem
Grab's GrabDefence risk platform ingests large volumes of data from many upstream services, and any discrepancy or missing data directly weakens fraud detection. The team needed to detect upstream data anomalies and incompleteness quickly across hundreds of data points arriving in inconsistent nested JSON structures.

## Approach / System design
A three-tier streaming observability pipeline: Apache Flink standardizes and aggregates the data in real time, Datadog handles monitoring and anomaly detection on the aggregated series, and Slack delivers alerts to on-call teams. Flink SQL's JSONEXPLOAD function deconstructs and flattens nested JSON into tabular rows, which are aggregated in 5-minute tumbling windows before being shipped to Datadog, where built-in anomaly detection with configurable thresholds watches each series.

## Key decisions
- Flatten inconsistent nested JSON with Flink SQL rather than writing per-schema parsing code, so disparate formats get one consistent analysis path.
- Aggregate in 5-minute tumbling windows to balance detection latency against noise.
- Organize monitors by upstream service stream rather than individual data points, reducing cognitive load for on-call engineers.
- Reuse Datadog's built-in anomaly detection instead of building a custom detector.

## Stack
Apache Flink (Flink SQL), Datadog, Slack.

## Results
Anomaly detection latency dropped from days-to-weeks to within the same day, and often within the hour. The pipeline is deployed on selected checkpoints of the risk platform.

## Takeaways
Pairing real-time stream aggregation with an off-the-shelf observability stack is a fast path to data-quality monitoring — the engineering effort goes into standardizing messy inputs and organizing alerts around sources, not into inventing detection algorithms.
