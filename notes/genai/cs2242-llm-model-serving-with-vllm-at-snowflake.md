---
id: cs2242
title: LLM Model Serving with vLLM at Snowflake
company: Snowflake
primary_category: genai
sub_category: inference-opt
year: 2025
source_url: https://www.snowflake.com/en/engineering-blog/llm-model-serving-vllm-inference/
tags: [vllm, llm-serving, inference, continuous-batching, paged-attention]
---

# LLM Model Serving with vLLM at Snowflake
**Snowflake** · 2025 · [source](https://www.snowflake.com/en/engineering-blog/llm-model-serving-vllm-inference/)

## Problem
Organizations deploying open-source LLMs in production face GPU infrastructure management, inference-optimization complexity, and data-security concerns. Customers wanted the flexibility of open models without the operational burden — and without data leaving their security perimeter.

## Approach / System design
Snowflake built Model Serving on Snowpark Container Services (SPCS) as a highly scalable inference service integrated with its existing Model Registry. vLLM is the inference engine, providing PagedAttention for dynamic GPU memory management and continuous batching, with streaming output support. Models are onboarded from Hugging Face with one-click import, and the serving containers run airgapped inside the customer's Snowflake account perimeter.

## Key decisions
- Airgapped container runtime within the account perimeter, keeping model weights and data inside the security boundary.
- Remote logging via CPU compute pools during model registration, avoiding the need for expensive GPUs just to onboard a model.
- OpenAI-compatible API across SQL, Python, and REST interfaces for a familiar developer experience.
- Runtime inference parameters (temperature, max_tokens) decoupled from the model signature so they can be set dynamically per request.

## Stack
vLLM inference engine; Snowpark Container Services; Snowflake Model Registry; Hugging Face model integration; OpenAI-compatible API; H200 GPUs for large models.

## Results
2.2x-2.3x better P99 latency and time-to-first-token versus Databricks across concurrency levels, and superior scaling versus Baseten at high concurrency. A 700GB model downloaded in 83 seconds (67.5 Gbps sustained), with effective serving of 700GB-class models on H200 GPUs.

## Takeaways
Separating inference cost from token-based pricing, routing specialized tasks to optimized models, and keeping data inside a secure perimeter are the compelling levers for enterprise LLM serving. Building on vLLM plus existing container and registry infrastructure avoided reinventing the serving core.
