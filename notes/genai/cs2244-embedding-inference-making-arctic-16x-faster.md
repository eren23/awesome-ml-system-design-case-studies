---
id: cs2244
title: "Embedding Inference: Making Arctic 16x Faster"
company: Snowflake
primary_category: genai
sub_category: inference-opt
year: 2025
source_url: https://www.snowflake.com/en/blog/engineering/embedding-inference-arctic-16x-faster/
tags: [embeddings, inference-optimization, arctic, embedding-model, throughput]
---

# Embedding Inference: Making Arctic 16x Faster
**Snowflake** · 2025 · [source](https://www.snowflake.com/en/blog/engineering/embedding-inference-arctic-16x-faster/)

## Problem
Snowflake processes trillions of tokens per month through embedding models for Cortex AI services such as semantic search and fraud detection, across both real-time and batch workloads. Profiling showed GPU inference accounted for only about 10% of total compute time — roughly 90% was CPU overhead. Two bottlenecks dominated: sequential tokenization on CPU left the GPU idle waiting for token IDs, and serializing embedding outputs to Protobuf for gRPC responses was throttled by Python's GIL and lack of SIMD vectorization.

## Approach / System design
Three targeted optimizations on top of vLLM. First, little-endian byte encoding: raw bytes produced with NumPy vectorization replaced Protobuf's repeated-float format, exploiting native CPU endianness to eliminate memory copies. Second, disaggregated tokenization: a two-stage pipeline where pretokenization passes token IDs onward, so tokenization and inference run concurrently across different requests. Third, multi-replica GPU execution: multiple identical model instances on a single GPU to soak up idle streaming multiprocessors and memory.

## Key decisions
- Profile first: flame-graph analysis exposed CPU bottlenecks that GPU-centric intuition had masked.
- Attack serialization and tokenization rather than the model — pipeline parallelism over architectural overhaul.
- Pack multiple replicas per GPU instead of assuming one model instance saturates the device.
- Open-source the work as the Arctic Inference vLLM plugin rather than keeping it internal.

## Stack
vLLM v0.8.3; A10g GPUs in production, H200 for benchmarks; snowflake-arctic-embed-m-v1.5 at FP16; NumPy vectorization; gRPC frontend; released as the Arctic Inference plugin.

## Results
On Cortex's A10g baseline: 3x overall throughput improvement and 230,000 tokens/second sustained. Open-source benchmarks on H200: 16x higher throughput on short sequences (50 tokens), 4.2x on long sequences (512 tokens), 16x cost reduction per trillion tokens, and 2.4x faster than Text Embeddings Inference on short sequences.

## Takeaways
Systematic profiling beats GPU-centric assumptions — the bottleneck was CPU work around the model. Disaggregating sequential stages yields large gains without touching the architecture, and optimized expensive hardware (H200) can end up cheaper per token than nominally cheaper instances.
