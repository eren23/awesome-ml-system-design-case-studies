---
id: cs2290
title: Turbocharging LinkedIn's Recommendation Systems with SGLang
company: LinkedIn
primary_category: rec
sub_category: ranking
year: 2025
source_url: https://www.linkedin.com/blog/engineering/ai/turbocharging-linkedins-recommendation-systems-with-sglang
tags: [sglang, llm-inference, radix-attention, kv-cache, throughput, recommendation-serving]
---

# Turbocharging LinkedIn's Recommendation Systems with SGLang
**LinkedIn** · 2025 · [source](https://www.linkedin.com/blog/engineering/ai/turbocharging-linkedins-recommendation-systems-with-sglang)

## Problem
LinkedIn's LLM-based recommendation ranking scored candidate items one at a time, so the lengthy member context — system prompt, profile, interaction history — was re-processed for every candidate. Under high traffic and strict latency budgets, that repeated prefill work became the dominant cost.

## Approach / System design
The team built Multi-Item Scoring (MIS) on top of SGLang: multiple candidate items are concatenated after a single shared member prefix into one prompt, and the whole set is scored in one inference pass. This required modifying attention kernels and SGLang's serving framework to handle prefix reuse correctly and extract per-item scores. They layered on a "Knock-Knock" technique that hides prefill latency by precomputing the member-context prefill while candidate retrieval is still running, so scoring starts warm.

## Key decisions
- Modified FlashAttention 2 and 3 kernels to support the custom attention masks multi-item scoring needs.
- Adopted FlashAttention 3 as the default backend for better long-context performance.
- Switched from online FP8 quantization to per-token FP8 scaling to recover accuracy while keeping the speed benefit.
- Contributed the kernel and framework changes upstream to open-source SGLang rather than maintaining private patches.

## Stack
SGLang, FlashAttention 2/3, FlashInfer attention kernels, FP8 quantization, gRPC streaming.

## Results
69% latency reduction from multi-item scoring versus the single-item baseline; +11% from the FA3 kernel work; +5% from upstream SGLang improvements (v0.4.1 to v0.4.3); +9% from per-token FP8. The Knock-Knock prefill overlap cut end-to-end latency a further 38% (520ms to 200ms). Overall, time-to-first-token dropped 3–4x.

## Takeaways
When LLMs rank candidates, the shared context is the workload — restructure the prompt so it's computed once. Kernel-level investment (attention masks, FP8 scaling) was necessary to make the architectural idea real, and upstreaming those changes meant the production system tracks the open-source project instead of diverging from it.
