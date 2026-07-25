---
id: cs2112
title: "Introducing Bento, Snap's ML Platform"
company: Snap
primary_category: data
sub_category: feature-store
year: 2025
source_url: https://eng.snap.com/introducing-bento
tags: [ML platform, feature generation, training data, model deployment, billion-scale, Snapchat]
---

# Introducing Bento, Snap's ML Platform
**Snap** · 2025 · [source](https://eng.snap.com/introducing-bento)

## Problem
Snap runs ML for hundreds of millions of users — on the order of hundreds of models trained per day and more than 1B predictions per second — primarily for ranking and recommendation. The platform had to solve two things at once: raise ML development throughput for practitioners and keep production serving scalable and cost-effective at that volume.

## Approach / System design
Bento covers the full ML lifecycle through four integrated pieces. Feature and training data generation aggregates event streams with Apache Spark (the Robusta platform), landing features in offline Apache Iceberg tables and in online key-value stores. Model training runs Kubeflow workflows on GKE or Vertex AI Pipelines, structured into composable layers (core framework, user model code, training configuration) for fast experimentation. ML production deploys models behind RPC services with specialized inference engines tuned for high-fanout ranking, plus a retrieval service that hydrates documents upstream for large-corpus scenarios. A control plane and custom monitoring provide experiment management UI and anomaly detection over predictions and features.

## Key decisions
- Instance-local feature stores co-located with inference engines, avoiding distributed lookups on the scoring path to cut latency.
- A dedicated retrieval service for document hydration in large-corpus ranking.
- Optimized, hardware-specific model export targeting GPUs/TPUs.
- Automated incremental training with continuous deployment gated on validation.
- Custom Protobuf deserialization, which cut latency by 2x and costs by 10x.

## Stack
Apache Spark, Apache Iceberg, Google BigQuery, Kubeflow on Google Kubernetes Engine, Vertex AI Pipelines, TensorFlow/PyTorch/Keras, Google Cloud Storage, and a custom thread-optimized inference engine.

## Results
Reported scale figures: 100K+ training compute hours per day, single training jobs consuming ~1 PB, an 800 TB online feature store with 1 TB/s reads, 500+ deployed models, 10 trillion events processed per day, and >1B predictions per second.

## Takeaways
An internal platform lets Snap specialize for its dominant workloads (ranking/recommendation), integrate tightly with its proprietary stack, and support users better than external offerings. At this throughput, sustained optimization across model export, inference, and the data plane is what keeps the system cost-effective.
