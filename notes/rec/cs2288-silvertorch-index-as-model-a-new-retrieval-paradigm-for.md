---
id: cs2288
title: "SilverTorch: Index as Model — A New Retrieval Paradigm for Recommendation Systems"
company: Meta
primary_category: rec
sub_category: candidate-generation
year: 2026
source_url: https://engineering.fb.com/2026/05/26/ml-applications/silvertorch-index-as-model-new-retrieval-paradigm-recommendation-systems/
tags: [retrieval, unified-architecture, gpu, throughput, sigir-2026, index-as-model]
---

# SilverTorch: Index as Model — A New Retrieval Paradigm for Recommendation Systems
**Meta** · 2026 · [source](https://engineering.fb.com/2026/05/26/ml-applications/silvertorch-index-as-model-new-retrieval-paradigm-recommendation-systems/)

## Problem
Meta's retrieval stack for user-generated-content recommendations was a mesh of microservices — ANN search, filtering, reranking, scoring — each with its own latency overhead, version skew, and siloed development. Service-to-service hops and inconsistencies capped how much retrieval sophistication could fit inside a sub-100ms latency budget.

## Approach / System design
SilverTorch collapses the entire retrieval pipeline into one neural network: the "Index as Model" paradigm. Approximate nearest neighbor search, eligibility filtering, neural reranking, and composite scoring all become PyTorch modules inside a single model, eliminating inter-service data movement and making previously independent stages jointly optimizable. Even non-ML operations like eligibility filtering were re-expressed as model components — bloom filters live as tensors inside the model. Streaming update infrastructure keeps the in-model index fresh.

## Key decisions
- Pure PyTorch throughout: redesign legacy components as native modules rather than wrapping existing services.
- Rethink algorithms for GPU execution patterns instead of porting CPU implementations.
- Optimize a single GPU first, then scale out via document sharding and TorchRec for sparse tables.

## Stack
PyTorch; fused Int8 ANN search; bloom filters as model tensors for eligibility; TorchRec for distributed sparse embedding tables; streaming index-update infrastructure.

## Results
On an 80M-item corpus: 23.7x throughput over the multi-service baseline, 20.9x better compute cost efficiency (13.35x with reranking enabled), and 291–523x faster filtering than a CPU inverted index. Int8 quantization halves memory with no measurable recall loss.

## Takeaways
Unifying retrieval as one model removes the architectural bottleneck, letting sophisticated ranking move earlier in the pipeline. It also collapses the ML/infra codebase boundary — deployment of new ideas went from weeks to days — and provides a natural slot for future LLM-based retrieval components. Presented at SIGIR 2026.
