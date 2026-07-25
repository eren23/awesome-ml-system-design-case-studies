---
id: cs2259
title: Building a User Signals Platform at Airbnb
company: Airbnb
primary_category: mlops
sub_category: platform
year: 2026
source_url: https://medium.com/airbnb-engineering/building-a-user-signals-platform-at-airbnb-b236078ec82b
tags: [kafka, flink, real-time, streaming, feature-engineering, lambda-architecture, kv-store, user-signals]
---

# Building a User Signals Platform at Airbnb
**Airbnb** · 2026 · [source](https://medium.com/airbnb-engineering/building-a-user-signals-platform-at-airbnb-b236078ec82b)

## Problem
Airbnb wanted to personalize the guest experience across the booking journey, which requires capturing user engagement events (searches, listing views, bookings) in near real time. Building such pipelines demanded stream-processing expertise most product teams lacked, so Airbnb needed platform infrastructure that could process millions of events per second while staying accessible to engineers unfamiliar with streaming systems.

## Approach / System design
The User Signals Platform (USP) follows a Lambda architecture:
- **Online layer**: Flink jobs consume Kafka events, transform them with under 1 second end-to-end latency, and write results to a key-value store.
- **Offline layer**: Hive-based batch jobs handle data correction and backfill.
- **Serving layer**: A USP service fronts reads and queries.

The platform exposes three signal types: user signals (recent queryable activities like searches and views), user segments (dynamic cohorts with trigger criteria and expiration logic), and session engagements (windowed behavioral analysis using sliding/session windows). A config-first interface auto-generates Flink job templates and shared transforms from YAML-style definitions so teams define signals without writing bespoke pipeline code.

## Key decisions
- Chose Flink over Spark: true event-based streaming instead of micro-batching, avoiding added delay for personalization use cases.
- Append-only KV storage with processing timestamps as versions, guaranteeing idempotency under at-least-once processing semantics.
- Config-driven development to democratize stream processing: templates and shared transforms rather than per-team custom jobs.

## Stack
Apache Kafka (event ingestion), Apache Flink (stream processing) with RocksDB as the streaming state store, a key-value database for transformed signals, Hive for the offline/batch layer.

## Results
- Over 1 million events per second processed across 100+ Flink jobs.
- Serves ~70,000 queries per second.
- Meets the <1 second end-to-end latency target for personalization.

## Takeaways
Platformizing streaming infrastructure — config-first definitions over hand-built pipelines — is what drove adoption across teams. Operationally, standby task managers materially improved stability during failures, and tracking latency at each stage (event, ingestion, job, transform) proved essential for monitoring a near-real-time system.
