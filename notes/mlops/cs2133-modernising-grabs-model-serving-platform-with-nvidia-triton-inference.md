---
id: cs2133
title: Modernising Grab's model serving platform with NVIDIA Triton Inference Server
company: Grab
primary_category: mlops
sub_category: platform
year: 2025
source_url: https://engineering.grab.com/modernising-grab-model-serving-platform
tags: [model-serving, triton, inference, gpu, platform-migration]
---

# Modernising Grab's model serving platform with NVIDIA Triton Inference Server
**Grab** · 2025 · [source](https://engineering.grab.com/modernising-grab-model-serving-platform)

## Problem
Grab's Catwalk serving platform maintained separate inference stacks for ONNX, PyTorch, TensorFlow, and vLLM. The sprawl created significant technical debt, increased latency, reduced throughput, and escalating costs, and constrained deployment of larger models.

## Approach / System design
Grab consolidated onto NVIDIA Triton Inference Server as a unified inference engine via a phased, centrally managed migration. Two components made it a drop-in replacement: a Triton Server Manager that downloads models, verifies files, generates per-model configuration, launches Triton, and monitors health; and a Triton Proxy that translates legacy API requests to Triton endpoints so existing users needed no code changes.

## Key decisions
- Backward API compatibility and zero-downtime migration as hard requirements, including CLI compatibility with the existing ONNX runtime server.
- Centralized migration executed by the platform team rather than pushed onto individual model owners.
- ONNX Runtime tuning: intra-op thread counts pinned to physical CPU core counts.
- Enable Triton features like dynamic batching and model ensembling as platform capabilities.

## Stack
NVIDIA Triton Inference Server; ONNX, PyTorch, and TensorFlow backends; NVIDIA GPUs, CPU instances, and AWS Inferentia.

## Results
50% of online deployments migrated within 10 days. Triton handled 5x the throughput of the previous ONNX server; transformer p90 latency dropped from 120ms to 20ms; XGBoost models held 2ms average latency; critical systems saw 50% better tail latency. Costs fell up to 90% for certain models, averaging ~20% across 11 production services within 14 days post-migration.

## Takeaways
Delivering an infrastructure upgrade as a transparent, backward-compatible platform enhancement — proxy plus manager, no user code changes — is what made rapid adoption possible; the performance and cost wins followed from consolidation onto one tuned engine.
