---
id: cs2340
title: "Unveiling the Core of Instacart's Griffin 2.0: A Deep Dive Into the Model Serving Platform"
company: Instacart
primary_category: mlops
sub_category: platform
year: 2024
source_url: https://tech.instacart.com/unveiling-the-core-of-instacarts-griffin-2-0-a-deep-dive-into-the-model-serving-platform-4a7298c0a54e
tags: [model-serving, inference, kubernetes, centralized-serving, ml-platform]
---

# Unveiling the Core of Instacart's Griffin 2.0: A Deep Dive Into the Model Serving Platform
**Instacart** · 2024 · [source](https://tech.instacart.com/unveiling-the-core-of-instacarts-griffin-2-0-a-deep-dive-into-the-model-serving-platform-4a7298c0a54e)

## Problem
Under Griffin 1.0, every team ran its own Gunicorn-based model serving service. Common logic — feature loading, preprocessing, experimentation, monitoring, feature logging — was re-implemented per service, each team carried its own DevOps burden, and there was no standard way to deploy or A/B a model. Performance suffered too: the Ads pCTR model's P99 accounted for 15% of total ads serving latency, and Gunicorn's process-forking model loaded a copy of the model per worker process, making memory footprint linear in worker count.

## Approach / System design
Griffin 2.0 introduces a unified Model Serving Platform (MSP) with four components. The Proxy routes items to be scored using a routing config (application-layer, environment-agnostic: which worker endpoint serves which model/experiment arm) combined with a worker config (physical-layer, environment-sensitive: endpoint aliases to URLs), merges worker responses, and returns predictions in request order. Workers are single-tenant ECS services running one model each in a multi-container setup: the main container handles feature loading, preprocessing, and feature logging, while a TensorFlow Serving sidecar performs inference. The Control Plane manages deployments — publishing a model, generating worker configs, relaunching workers on model promotion, and auto-creating Datadog metrics and alerts. The Model Registry stores artifacts that embed Protobuf-serialized feature-location configs (which features come from the request vs. the feature store) and feature-preprocessor configs (DAGs over a unified Python preprocessor library shared by training and serving). Experimentation is configuration-driven with a traffic-splitting key, batching on proxy-to-worker calls trims tail latency, and Arize monitors prediction accuracy, score distributions, and train/serve drift.

## Key decisions
- Go for the serving service instead of Python/Gunicorn — compiled, with a concurrency model suited to high-concurrency serving and one model load per instance.
- Single-tenancy per worker for failure isolation, fast restarts, and implementation simplicity.
- Separation of environment-agnostic routing config from environment-sensitive worker config, with config changes gated by ML-infra code review.
- Control-Plane-triggered worker relaunch on promotion to close the model-version-discrepancy window that previously required custom Airflow restart jobs.
- A single Python preprocessor library, framework-agnostic, used identically in training and serving to kill skew.
- Sidecar-based model runtime so frameworks beyond TensorFlow can slot in later.

## Stack
Go (Proxy/Worker), TensorFlow Serving sidecars, Amazon ECS, S3 for artifacts, Protobuf configs and APIs, Python preprocessor library, Datadog for real-time monitoring, Arize for model performance monitoring, near-real-time feature logging pipeline.

## Results
On the Ads pCTR model, MSP cut both P99 and P50 serving latency by over 80% versus the Gunicorn service, shrinking pCTR's share of total ads serving latency from 15% to 3%. Memory footprint and EC2 costs dropped substantially since each instance loads one model copy. Time to launch an ML model fell from weeks to minutes, with experimentation, feature loading, and preprocessing all configuration-driven.

## Takeaways
- Consolidating per-team serving services into one platform eliminates duplicated logic and DevOps overhead while standardizing deployment and experimentation.
- Language/runtime choice matters at serving scale: Go's concurrency model beat forked Python processes on both latency and memory.
- Embedding feature and preprocessing configs in the model artifact makes serving self-describing and keeps training/serving consistent.
- Configuration-driven self-service with a gatekeeping review process balances velocity and ownership.
