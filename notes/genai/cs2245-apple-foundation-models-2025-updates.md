---
id: cs2245
title: Apple Foundation Models 2025 Updates
company: Apple
primary_category: genai
sub_category: llm
year: 2025
source_url: https://machinelearning.apple.com/research/apple-foundation-models-2025-updates
tags: [on-device, foundation-models, apple-intelligence, model-updates, privacy]
---

# Apple Foundation Models 2025 Updates
**Apple** · 2025 · [source](https://machinelearning.apple.com/research/apple-foundation-models-2025-updates)

## Problem
Apple Intelligence needs generative models that run under strict privacy constraints: an on-device model (~3B parameters) efficient enough for Apple silicon with low latency, plus a capable server model — both supporting 15 languages with improved reasoning, tool use, and multimodal understanding, without training on private user data.

## Approach / System design
The ~3B on-device model is split into two blocks with a 5:3 depth ratio; block 2 shares the KV caches produced by block 1's final layer, cutting KV-cache memory 37.5%. The server model uses a new Parallel-Track Mixture-of-Experts (PT-MoE) architecture: independent transformer tracks with their own MoE layers that synchronize only at input/output boundaries, cutting synchronization overhead from 2L to L/D (87.5% reduction at D=4). Vision uses ViT-g (1B) on server and ViTDet-L (300M) on device, with a Register-Window mechanism capturing local detail plus global context and an adapter aligning image features to the LLM. Training is multi-stage (text-only, then visual alignment, then domain continued pre-training); the server model trained from scratch on 14T text tokens; the on-device model was distilled from a teacher built by sparse-upcycling a 64-expert MoE, cutting teacher training cost 90%. Post-training combines SFT with RLHF using a reward-variance-based prompt-selection algorithm. Aggressive quantization: 2-bpw decoder weights on device via QAT; 3.56-bpw on server via ASTC texture compression decompressed by dedicated GPU hardware; 4-bit embeddings and 8-bit KV caches on both.

## Key decisions
- KV-cache sharing and PT-MoE as architectural routes to capability-per-watt rather than raw scale.
- Distillation from a sparse-upcycled MoE teacher instead of an expensive dense teacher.
- ASTC texture compression for server weights, exploiting existing GPU decompression hardware to avoid compute overhead.
- Tokenizer vocabulary grown 100k→150k and multilingual RLHF for 15-language support (16:9 win/loss in human evals).
- Training data of 10B+ image-text pairs, 175M interleaved image-text documents (550M+ images), and 5B+ synthetic caption pairs — no private user data.
- Developer access via the Foundation Models framework: Swift-macro guided generation (constrained decoding), tool calling, and rank-32 adapter training via a Python toolkit.

## Stack
Custom transformer/PT-MoE architectures on Apple silicon; QAT and ASTC quantization; ViT-g / ViTDet-L vision encoders; SFT + RLHF pipeline; Foundation Models framework with Swift guided generation and adapter toolkit.

## Results
Quantization cost little: on-device ~4.6% regression on MGSM but +1.5% on MMLU; server −2.7% MGSM, −2.3% MMLU. Human evals: the on-device model performs favorably against the slightly larger Qwen-2.5-3B across all languages and is competitive with Qwen-3-4B and Gemma-3-4B in English; the server model outperforms Qwen-2.5-VL on image understanding at less than half the inference FLOPS.

## Takeaways
Architectural innovation (cache sharing, parallel-track MoE) buys efficiency without proportional resource growth; 2-bit weights are viable with careful quantization-aware training; multilingual quality demands intentional per-language evaluation, safety data, and cultural expertise rather than translation alone; and privacy and capability can coexist — on-device inference delivers both. Framework-level developer access (guided generation, tool calling, adapters) is how the models reach third-party apps.
