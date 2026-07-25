---
id: cs2206
title: Building A Declarative Real-Time Feature Engineering Framework at DoorDash
company: DoorDash
primary_category: data
sub_category: feature-store
year: 2025
source_url: https://careersatdoordash.com/blog/building-a-declarative-real-time-feature-engineering-framework/
tags: [Flink, declarative-features, YAML-config, Protobuf, streaming, feature-serving, real-time, Riviera, feature-engineering]
---

# Building A Declarative Real-Time Feature Engineering Framework at DoorDash
**DoorDash** · 2025 · [source](https://careersatdoordash.com/blog/building-a-declarative-real-time-feature-engineering-framework/)

## Problem
DoorDash's ML models ran mostly on batch features from historical ETLs, leaving real-time signal on the table. Building a bespoke Flink application per feature pipeline created three bottlenecks: Flink's steep learning curve limited development to specialized engineers (accessibility), boilerplate dominated the deployed code with business logic a small fraction (reusability), and bundling multiple features into one application made resource management inefficient (isolation).

## Approach / System design
DoorDash built Riviera, a declarative real-time feature engineering framework in two layers. Layer one is a Flink-as-a-service platform: a customized Flink runtime on Kubernetes plus a reusable library abstracting common configuration, with two-level YAML configs separating infrastructure concerns from user concerns. Layer two is Riviera itself — a generified Flink application instantiated from declarative YAML, so feature authors express transformation logic in Flink SQL and never write custom Flink code. Features consume Kafka/Protobuf streams and land in Redis for serving, with S3 and Snowflake as additional sinks.

## Key decisions
- Chose Flink SQL as the DSL for transformations, riding community-driven performance and feature improvements rather than inventing a custom language.
- Built a reflection-based deserialization layer converting Protobuf into flattened tabular schemas, since Flink SQL lacked native Protobuf support.
- Used Flink interval joins instead of in-memory caches to handle data-arrival disparity and complex state.
- Ran each feature pipeline as its own instantiated application for isolation and independent scaling.

## Stack
Apache Flink (SQL) on Kubernetes, YAML configuration, Protobuf (primary) and Avro serialization, Kafka sources, Redis feature serving, S3 and Snowflake sinks, gRPC.

## Results
- Feature development iteration reduced from a few weeks to a few hours; new sources/sinks adaptable within days.
- Feature-pipeline codebase shrank by over 70%.
- Parallelism for delivery ASAP-time feature computation scaled from 1 to 15 workers.
- Sustained 5,000+ events/second on joins spanning ~300 columns over 4-hour windows.

## Takeaways
Declarative abstraction democratizes streaming feature engineering: hiding Flink behind SQL-in-YAML let non-specialists ship real-time features. Most streaming-pipeline code is undifferentiated scaffolding that a platform can absorb once, and per-pipeline isolation plus platform-managed state unlocks much higher parallelism than hand-rolled applications.
