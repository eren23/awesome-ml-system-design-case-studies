---
id: cs2262
title: Accelerating AI Inference for 3D Creation on Roblox
company: Roblox
primary_category: mlops
sub_category: serving
year: 2025
source_url: https://about.roblox.com/newsroom/2025/06/accelerating-ai-inference-roblox-3d-creation
tags: [inference-optimization, cuda-graphs, kv-cache, transformer, 3d-generation, latency, gpu-optimization]
---

# Accelerating AI Inference for 3D Creation on Roblox
**Roblox** · 2025 · [source](https://about.roblox.com/newsroom/2025/06/accelerating-ai-inference-roblox-3d-creation)

## Problem
Roblox's Cube 3D autoregressive transformer generates 3D objects from text prompts, but naive inference took 60.5ms per token and about 31 seconds per object — far too slow for an interactive creation tool. Profiling showed the bottleneck was CPU–GPU scheduling inefficiency: the GPU sat idle while the CPU prepared the next batch of work.

## Approach / System design
Cube 3D is an autoregressive transformer with a dual-stream decoder: parallel attention streams process condition (text) tokens and shape tokens separately. Because this differs from standard LLM architectures, off-the-shelf inference frameworks didn't fit, and the team built a custom inference path with two main optimizations:
- **CUDA Graphs**: record the sequence of GPU operations once and replay it, eliminating per-operation CPU launch/scheduling overhead. This requires fixed batch and input sizes — a flexibility-for-efficiency trade.
- **KV caching**: cache key/value matrices for previously generated tokens so each new token avoids recomputing attention over the whole sequence.

## Key decisions
- Profile first: identify that scheduling overhead, not raw compute, dominated inference time.
- Accept CUDA Graphs' fixed-shape constraints in exchange for removing CPU dispatch overhead (2.9x speedup on time-per-output-token by itself).
- Build custom inference for the dual-stream architecture instead of forcing the model into generic LLM serving frameworks.
- Stack the optimizations: CUDA Graphs plus KV caching compound to the full gain.

## Stack
Custom dual-stream transformer decoder, CUDA / CUDA Graphs, KV caching, GPU-accelerated inference pipeline.

## Results
- Per-token generation: 60.5ms → 7.8ms (7.8x speedup).
- Full object generation: 31s → 4s (~87% reduction); ~7s end-to-end with post-processing.
- Shipped before public launch; 578,000+ objects generated post-launch.

## Takeaways
In autoregressive generation, per-operation overhead can dominate total inference time — the fix is amortizing scheduling (CUDA Graphs), not just faster kernels. Non-standard architectures need tailored inference work; the payoff is latency low enough to keep human creators in an interactive iteration loop.
