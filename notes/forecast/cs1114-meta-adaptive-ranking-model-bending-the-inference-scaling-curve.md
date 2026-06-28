---
id: cs1114
title: "Meta Adaptive Ranking Model: Bending the Inference Scaling Curve to Serve LLM-Scale Models for Ads"
company: Meta
primary_category: forecast
sub_category: eta-prediction
year: 2026
source_url: https://engineering.fb.com/2026/03/31/ml-applications/meta-adaptive-ranking-model-bending-the-inference-scaling-curve-to-serve-llm-scale-models-for-ads/
tags: [ad ranking / targeting, ranking, inference]
---

# Meta Adaptive Ranking Model: Bending the Inference Scaling Curve to Serve LLM-Scale Models for Ads
**Meta** · 2026 · [source](https://engineering.fb.com/2026/03/31/ml-applications/meta-adaptive-ranking-model-bending-the-inference-scaling-curve-to-serve-llm-scale-models-for-ads/)

## Problem
Scaling ads ranking models toward LLM-scale complexity hits an "inference trilemma": more model sophistication, sub-second latency, and cost efficiency at billions-of-users scale all pull against each other.

## Approach / System design
Meta Adaptive Ranking Model (MARM) replaces one-size-fits-all inference with request-level routing that dynamically matches model complexity to each request's context and intent, so each request hits the most effective yet efficient model within latency bounds. Three pillars:
1. Inference-efficient scaling — LLM-equivalent complexity (~O(10) GFLOPs/token) but ~10x faster than standard LLM inference within ~O(100ms) latency; request-oriented optimization computes user signals once per request (not per ad candidate), turning cost from linear to sub-linear; request-oriented sequence scaling processes long behavior sequences centrally and shares results across candidates.
2. Model-system codesign — ~35% Model FLOPs Utilization across heterogeneous hardware; selective FP8 quantization; hardware-aware graph/kernel specialization with operator fusion.
3. Reimagined serving — ~O(1T)-parameter models via unified embedding tables; multi-GPU sharded embeddings; fast model loading (<10 min) and SM-utilization-based autoscaling.

## Key decisions
- Compute per-request signals once and share across ad candidates to break the linear cost-per-candidate scaling.
- Selective (not blanket) FP8 quantization to keep throughput without degrading quality.
- Architecture: Wukong Turbo (evolved from Wukong's factorization machines, sequence learning, cross-layer attention).

## Stack
Wukong Turbo architecture; FSDP and DDP distributed training; FP8 quantization; operator/kernel fusion; unified/sharded embedding tables; GPU-native Top-K kernel reducing O(N log N) to O(N); compact tuple data formats; No-Bias technique to drop unstable terms.

## Results
Since the Instagram launch in Q4 2025: +3% ad conversions and +5% ad click-through rate for targeted users.

## Takeaways
The lever for serving LLM-scale ranking affordably is request-centric computation sharing — compute user/sequence signals once per request, not per candidate — which bends the scaling curve from linear to sub-linear, combined with deep model-system codesign (FP8, kernel fusion, MFU) and sharded trillion-parameter serving.
