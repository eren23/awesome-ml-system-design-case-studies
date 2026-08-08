---
id: cs2426
title: In-House LLM Serving at Netflix
company: Netflix
primary_category: mlops
sub_category: platform
year: 2026
source_url: https://netflixtechblog.com/in-house-llm-serving-at-netflix-a5a8e799ea2c
tags: [vLLM, LLM serving, TensorRT-LLM, model serving, inference infrastructure, unified serving, gRPC, LLMOps]
---

# In-House LLM Serving at Netflix
**Netflix** · 2026 · [source](https://netflixtechblog.com/in-house-llm-serving-at-netflix-a5a8e799ea2c)

## Problem
Netflix's AI Platform needed to serve a diverse range of model types — from traditional XGBoost ensembles to large language models — under a single, coherent infrastructure. Running multiple serving systems in parallel created operational fragmentation, and TensorRT-LLM, the previous LLM serving engine, added complexity that was difficult to maintain and extend across teams.

## Approach / System design
Netflix migrated its LLM serving stack from TensorRT-LLM to vLLM as the standard serving engine and unified all model types under a single gRPC-based serving pipeline. This consolidated infrastructure allows the AI Platform team to operate one serving layer regardless of model type, from lightweight gradient-boosted trees to multi-billion parameter language models.

## Key decisions
Choosing vLLM as the paved path reduces the per-model operational overhead that teams had previously incurred when deploying LLMs, and vLLM's active open-source development means Netflix benefits from upstream improvements without building proprietary inference optimizations. Standardizing on gRPC for the serving protocol provides consistent latency and streaming semantics across all model types.

## Stack
vLLM (primary LLM serving engine), TensorRT-LLM (previous engine, replaced), gRPC-based unified serving pipeline, XGBoost and other model types served via same infrastructure.

## Results
Not covered in the source.

## Takeaways
Consolidating LLM and non-LLM models onto a single serving platform dramatically reduces operational complexity and the number of distinct systems an ML platform team must maintain. vLLM's growing ecosystem makes it a viable paved-path choice for organizations that need flexible, actively maintained LLM serving without the overhead of a fully custom stack. Standardizing on a common RPC protocol across all model types simplifies client integration and enables consistent observability.
