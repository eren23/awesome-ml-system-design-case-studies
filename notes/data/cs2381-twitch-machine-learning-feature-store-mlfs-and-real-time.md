---
id: cs2381
title: Twitch Machine Learning Feature Store (MLFS) and Real-Time Feature Engineering
company: Twitch
primary_category: data
sub_category: feature-store
year: 2023
source_url: https://blog.twitch.tv/en/2023/09/28/twitch-state-of-engineering-2023/
tags: [feature-store, real-time, aws-kinesis, streaming, ml-infrastructure]
---

# Twitch Machine Learning Feature Store (MLFS) and Real-Time Feature Engineering
**Twitch** · 2023 · [source](https://blog.twitch.tv/en/2023/09/28/twitch-state-of-engineering-2023/)

## Problem
Twitch's product teams each build ML models (recommendations, personalization) but lacked a centralized way to manage and share features across teams. Batch-only feature pipelines also meant time-critical applications had to wait on stale data.

## Approach / System design
The ML Infrastructure (MLI) team runs four core systems: a Model Registry (stores model metadata and isolates training pipelines from production services), a Model Deployment system (CI/CD for models with testing, canary environments, and automated rollout/rollback), MLFS (the feature management layer), and Real-Time Feature (the streaming component). MLFS operates in a federated fashion: individual teams manage their own instances while retaining shared access, and the system supports multiple data backends. Real-Time Feature ingests streaming data through AWS Kinesis and lands features in MLFS with seconds of latency, so models can consume fresh signals without batch delays.

## Key decisions
- Federated feature-store ownership: teams run their own MLFS instances but features remain shareable across the org, avoiding a central bottleneck.
- Pluggable data backends rather than a single mandated store.
- A dedicated streaming path (Kinesis → MLFS) alongside batch, to serve time-critical personalization use cases.
- Separating the model registry from production services so training pipelines are decoupled from serving.

## Stack
AWS Kinesis for streaming ingestion; MLFS (in-house feature store) with multiple backend support; in-house model registry and model deployment/CI-CD tooling with canary and rollback support.

## Results
Streaming features become available in MLFS with seconds of latency. The infrastructure supports serving fresh, personalized recommendations across billions of daily requests. No further quantitative results are given in the source.

## Takeaways
- A federated feature store balances team autonomy with cross-team feature reuse.
- Real-time feature availability (seconds, not hours) unlocks time-critical ML use cases.
- Treating model deployment like software CI/CD (canaries, automated rollback) keeps a continuous learn–infer–observe loop safe at scale.
