---
id: cs1790
title: Anomaly Detection in Zipkin Trace Data
company: Salesforce
primary_category: anomaly
sub_category: outlier-detection
year: 2025
source_url: https://engineering.salesforce.com/anomaly-detection-in-zipkin-trace-data-87c8a2ded8a1/
tags: [distributed-tracing, zipkin, latency, microservices, correlation]
---

# Anomaly Detection in Zipkin Trace Data
**Salesforce** · 2025 · [source](https://engineering.salesforce.com/anomaly-detection-in-zipkin-trace-data-87c8a2ded8a1/)

## Problem
Salesforce's microservices architecture generates large volumes of distributed traces via Zipkin, and manually identifying which services contribute to elevated end-to-end latency is impractical at scale. Engineers needed an automated approach to analyze span data, surface outlier services with abnormal latency distributions, and identify chokepoints in the service call graph.

## Approach / System design
Salesforce built an offline Python-based analysis pipeline that ingests Zipkin spans, computes completeness metrics, and constructs call-graph visualizations using NetworkX. Latency distributions are log-transformed to normalize skewed data, and Pearson correlation is applied across services to detect pairs with statistically linked latency spikes, pinpointing services that propagate latency through the graph.

## Key decisions
Log-transforming latency before computing statistics accounts for the exponential tail behavior common in microservice latency distributions, making mean and correlation measures more meaningful. Choosing NetworkX for call-graph construction allows the team to leverage graph algorithms to identify structural chokepoints — nodes with high centrality that affect many downstream services.

## Stack
Python, Zipkin (distributed tracing), NetworkX (call-graph visualization and analysis), log-transform normalization, Pearson correlation.

## Results
Not covered in the source.

## Takeaways
Distributed trace data contains rich structural information about service dependencies that aggregate metrics alone cannot provide. Log-transforming latency before statistical analysis is important for correctly identifying outlier services whose latency follows an exponential rather than Gaussian distribution. Combining graph-based call-path visualization with pairwise correlation analysis helps engineers quickly narrow down latency root causes in complex microservice topologies.
