---
id: cs1800
title: Improved Alerting with Atlas Streaming Eval
company: Netflix
primary_category: anomaly
sub_category: alerting
year: 2023
source_url: https://netflixtechblog.com/improved-alerting-with-atlas-streaming-eval-e691c60dc61e
tags: [atlas, streaming-eval, sli-metrics, telltale, correlation]
---

# Improved Alerting with Atlas Streaming Eval
**Netflix** · 2023 · [source](https://netflixtechblog.com/improved-alerting-with-atlas-streaming-eval-e691c60dc61e)

## Problem
Netflix's Atlas metrics platform was evaluating alert expressions by periodically polling stored metric data, which did not scale to the hundreds of thousands of alert expressions the organization needed. The polling model also introduced evaluation lag, making it slower to detect service-level indicator anomalies and reducing the speed of incident response.

## Approach / System design
Netflix moved alert evaluation from a polling model to a streaming model, where Atlas continuously evaluates alert expressions against an incoming stream of metric data rather than querying historical snapshots. The Telltale anomaly correlation system was also migrated to consume real-time Atlas streaming data, enabling it to detect SLI degradations and correlate anomalies across services as they occur rather than after the fact.

## Key decisions
Streaming evaluation eliminates the polling interval as a floor on detection latency, making it possible to alert on metric deviations within seconds of their occurrence. Integrating Telltale with the same streaming pipeline ensures that correlation happens on the freshest available data and shares infrastructure with the alerting system.

## Stack
Atlas (Netflix metrics platform), Atlas Streaming Eval engine, Telltale (SLI anomaly detection and correlation system).

## Results
Not covered in the source.

## Takeaways
Migrating alerting from a poll-based to a stream-based evaluation model is necessary to scale to very large numbers of alert expressions without proportionally increasing query load on the metrics store. Real-time streaming evaluation meaningfully reduces time-to-detect for SLI anomalies compared to polling. Sharing a streaming pipeline between alerting and correlation tools improves both freshness and infrastructure efficiency.
