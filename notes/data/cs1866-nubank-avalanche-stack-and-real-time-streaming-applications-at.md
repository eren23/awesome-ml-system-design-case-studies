---
id: cs1866
title: Nubank — Avalanche Stack and Real-Time Streaming Applications at Nu
company: Nubank
primary_category: data
sub_category: data-pipeline
year: 2025
source_url: https://building.nubank.com/avalanche-stack-and-real-time-streaming-applications-at-nu/
tags: [streaming, flink, kafka, pinot, kubernetes, fraud-detection, real-time-features]
---

# Nubank — Avalanche Stack and Real-Time Streaming Applications at Nu
**Nubank** · 2025 · [source](https://building.nubank.com/avalanche-stack-and-real-time-streaming-applications-at-nu/)

## Problem
Nubank needed a standardized, production-grade platform for real-time streaming workloads spanning fraud detection, risk scoring, and feature computation. Without a shared infrastructure stack, teams built bespoke solutions that were difficult to operate, scale, and integrate with one another.

## Approach / System design
The Avalanche stack consolidates real-time streaming on four components: Kubernetes for container orchestration and horizontal scaling, Apache Kafka as the distributed event bus, Apache Flink for stateful stream processing with exactly-once semantics, and Apache Pinot for serving aggregated features at low latency. The stack is designed as a unified platform that application teams deploy onto rather than assemble themselves, with standardized deployment patterns and observability built in.

## Key decisions
Standardizing on a single opinionated stack rather than allowing each team to choose its own components reduced operational overhead and made it easier to share tooling, runbooks, and expertise across teams. Flink was selected for stateful stream processing because of its mature support for event-time windowing and exactly-once guarantees, which are critical for financial use cases.

## Stack
Kubernetes, Apache Kafka, Apache Flink, Apache Pinot.

## Results
The Avalanche stack powers fraud detection models that achieved a 13% improvement in identification of high-risk loan applicants.

## Takeaways
Standardizing streaming infrastructure into an opinionated platform accelerates team velocity by eliminating repeated infrastructure decisions while concentrating operational expertise. Real-time feature computation over streaming data enables richer, more timely signals for risk models compared to batch-computed features.
