---
id: cs1865
title: Nubank — Feature Stores for Real-Time ML: Why and When to Centralize Feature Logic
company: Nubank
primary_category: data
sub_category: feature-store
year: 2026
source_url: https://building.nubank.com/feature-stores-for-real-time-ml-why-and-when-to-centralize-feature-logic/
tags: [feature-store, real-time, training-serving-skew, feature-registry, kafka, real-time-ml, feature-reuse, centralization]
---

# Nubank — Feature Stores for Real-Time ML: Why and When to Centralize Feature Logic
**Nubank** · 2026 · [source](https://building.nubank.com/feature-stores-for-real-time-ml-why-and-when-to-centralize-feature-logic/)

## Problem
When each ML team implements its own feature logic, the same business concepts get computed differently in training and serving pipelines, leading to training-serving skew and model degradation. Feature code duplication also prevents reuse, inflates maintenance burden, and makes it hard to audit what signals are being used across the organization.

## Approach / System design
Nubank centralizes feature logic in a feature store that supports two retrieval strategies: synchronous HTTP calls for low-latency online serving, and streaming retrieval via Kafka for use cases where features can be pre-computed and pushed downstream. A feature registry records which features exist, how they are defined, and which models consume them, enabling discovery and reuse across teams.

## Key decisions
Offering both HTTP and Kafka retrieval paths allowed the feature store to serve diverse latency and throughput requirements without forcing teams into a single access pattern. The feature registry was treated as a required artifact for publishing features rather than an optional documentation step, ensuring the catalog stayed current.

## Stack
Apache Kafka, HTTP APIs, feature registry.

## Results
Not covered in the source.

## Takeaways
Centralizing feature logic pays off when features are shared across multiple models or when training-serving consistency is critical—typically in real-time fraud and credit risk settings. The latency trade-offs of centralized retrieval must be weighed carefully against the consistency and reuse benefits, particularly for sub-100 ms serving requirements.
