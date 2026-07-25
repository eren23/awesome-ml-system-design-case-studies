---
id: cs2391
title: How Trustpilot built a real-time architecture for data enrichment using Gemma
company: Trustpilot
primary_category: genai
sub_category: fine-tuning
year: 2026
source_url: https://cloud.google.com/blog/topics/customers/how-trustpilot-built-a-real-time-architecture-for-data-enrichment-using-gemma
tags: [gemma, fine-tuning, apache-dataflow, vllm, streaming, ner, sentiment-analysis, real-time, open-weight]
---

# How Trustpilot built a real-time architecture for data enrichment using Gemma
**Trustpilot** · 2026 · [source](https://cloud.google.com/blog/topics/customers/how-trustpilot-built-a-real-time-architecture-for-data-enrichment-using-gemma)

## Problem
Trustpilot needs to enrich millions of user reviews per day in real time — named entity recognition, sentiment analysis, intent detection, topic classification — under strict latency and cost constraints. Per-token pricing on closed-model APIs was not viable for a mission-critical, high-volume pipeline.

## Approach / System design
A streaming Dataflow pipeline routes reviews through two decoupled endpoints: a FastAPI "classifier" endpoint handling pre/post-processing, prompt templating, and chaining logic, which calls a vLLM endpoint serving fine-tuned gemma-2-9b models on A100 GPUs (A2 VMs, EU region). Training data came from consensus annotations by Gemini 2.0/2.5 Pro and Flash teacher models over a stratified review corpus. Dataflow integrates natively via VertexAIModelHandlerJSON. Serving was tuned with vLLM engine parameters and dtypes, prefix caching, a reusable load-testing framework to size infrastructure, and autoscaling driven by request count plus vLLM queue depth.

## Key decisions
- Fine-tune an open-weight Gemma model instead of calling Gemini APIs: model independence (own the retraining lifecycle, no vendor/API-change exposure), predictable fixed infrastructure cost instead of variable token pricing, in-house MLOps competency, and continuity onto future base models.
- Teacher-model consensus labeling (multiple Gemini models) to build fine-tuning data cheaply at quality.
- Split business logic (classifier endpoint) from LLM inference (vLLM endpoint) so the two scale independently.
- Reserve A100 capacity in the EU rather than rely on on-demand, given GPU scarcity across dev/prod/training/inference needs.

## Stack
google/gemma-2-9b (fine-tuned), Gemini 2.0/2.5 Pro/Flash (teachers), vLLM on Agent Platform endpoints, A100 GPUs on A2 VMs, Google Cloud Dataflow, FastAPI, VertexAIModelHandlerJSON.

## Results
The pipeline processes millions of reviews daily in near real time, achieving accuracy only a few percentage points below the Gemini teacher consensus at "Gemini-like performance for a fraction of the cost" — exact cost figures are not disclosed. Pain points: no native private networking between the two endpoints, slow and opaque endpoint deployments, and EU GPU scarcity requiring reservations.

## Takeaways
- At high volume, fixed-cost self-hosted open-weight models beat per-token API economics while staying close to frontier quality.
- Teacher-consensus distillation is an efficient path to specialized small models.
- Decoupling orchestration from inference, plus load-test-driven sizing and queue-aware autoscaling, is what makes LLM serving production-grade.
