---
id: cs2291
title: Scaling LLM-Based Ranking Systems with SGLang at LinkedIn
company: LinkedIn
primary_category: rec
sub_category: ranking
year: 2026
source_url: https://www.linkedin.com/blog/engineering/ai/scaling-llm-based-ranking-systems-with-sglang-at-linkedin
tags: [sglang, prefill-only, llm-ranking, inference-optimization, cost-efficiency, open-source, kv-cache, inference-serving, shared-prefix, gpu]
---

# Scaling LLM-Based Ranking Systems with SGLang at LinkedIn
**LinkedIn** · 2026 · [source](https://www.linkedin.com/blog/engineering/ai/scaling-llm-based-ranking-systems-with-sglang-at-linkedin)

## Problem
LinkedIn's AI-powered search and recommendation features use LLMs as rankers: score hundreds of candidate items against one query under a sub-500ms P99 budget. This is a prefill-only workload — no token generation at all — yet standard generative serving stacks drag in sampling, decode loops, and per-request overhead that made production latency targets unreachable.

## Approach / System design
The team extended SGLang in four sequential stages. First, batching infrastructure: batch tokenization plus a "batch send" mechanism so batches survive the CPU-to-GPU handoff intact. Second, a dedicated scoring path that skips generation, sampling, and the decode loop entirely. Third, in-batch prefix caching so the shared query prefix's KV computation is reused across all items within a single forward pass. Fourth, Python runtime work: freezing the heap to eliminate garbage-collection stalls and moving to a multi-process serving architecture to sidestep GIL contention, with asyncio-driven dynamic batch aggregation.

## Key decisions
- Treat ranking as a first-class workload in the serving engine, not a degenerate case of generation.
- Optimize layer by layer (tokenization, GPU execution, memory reuse, Python runtime) rather than hunting for one silver bullet.
- Keep the ranking API inside the standard SGLang inference engine and upstream the changes, avoiding a forked codebase.

## Stack
SGLang (with LinkedIn's contributions upstreamed), PyTorch for profiling and kernel execution, ZMQ for inter-process communication, Python asyncio for dynamic batching, NVIDIA H100 GPUs.

## Results
Text-based ranking with a 375M decoder-only model went from 750 to 2,200 items/s/GPU (~3x); a 0.6B mixed-input ranker from 10k to 22k items/s/GPU (~2.2x). Dynamic batching cut embedding P99 latency from 4,583ms to 464ms (~10x), and the dedicated scoring path took a 0.6B model from 6,220ms to 454ms P99 (13.7x). All while holding P99 at or under 500ms.

## Takeaways
Profile ruthlessly — upstream CPU bottlenecks can erase GPU wins entirely. Gains compounded across layers; no single optimization sufficed. Prefill-only ranking has fundamentally different characteristics (no decode, high concurrency, long shared prefixes) than generation, and specializing for it inside the mainline engine — rather than fragmenting into a fork — let both LinkedIn and the open-source community benefit.
