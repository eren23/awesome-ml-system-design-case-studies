---
id: cs2243
title: Fast Speculative Decoding with vLLM and Arctic at Snowflake
company: Snowflake
primary_category: genai
sub_category: inference-opt
year: 2025
source_url: https://www.snowflake.com/en/engineering-blog/fast-speculative-decoding-vllm-arctic/
tags: [speculative-decoding, vllm, arctic, llm-inference, latency-optimization]
---

# Fast Speculative Decoding with vLLM and Arctic at Snowflake
**Snowflake** · 2025 · [source](https://www.snowflake.com/en/engineering-blog/fast-speculative-decoding-vllm-arctic/)

## Problem
Generation latency is a critical bottleneck for LLM applications. Existing speculative-decoding solutions do not fully exploit the highly repetitive output patterns of agentic workloads, and there was no standardized framework for training custom draft models and deploying them to production.

## Approach / System design
Snowflake AI Research built a two-pronged system. Suffix decoding maintains suffix trees over historical outputs to dynamically build speculative sequences from repetitive textual structure, at roughly 20 microseconds per token — well suited to agentic loops. A complementary speculative training pipeline provides standardized YAML-based recipes for training lightweight draft models (MLP and LSTM variants) that handle non-repetitive generation. The two methods are combined so mixed workloads (repetitive agentic plus conversational) are covered, and everything ships as a vLLM-compatible plugin.

## Key decisions
- Combine pattern-based (suffix tree) and learned (draft model) speculation instead of forcing a choice per workload.
- Greedy verification instead of rejection sampling.
- FP8 quantization, tensor parallelism, and optimized communication patterns in the serving path.
- Integrate as a vLLM plugin rather than forking vLLM.

## Stack
vLLM (v0.8.4 and v1); CUDA; MLP and LSTM draft-model architectures; suffix trees; evaluated with Llama 3.1-70B, Llama 3.3-70B, and Qwen2.5-32B.

## Results
On SWE-Bench (agentic): 4x faster decoding and 1.8-4.5x end-to-end speedup. On ShareGPT/HumanEval: 2.05x-2.45x speedup over the non-speculative baseline. Draft-model acceptance rates 3.1x higher than public MLP-Speculator baselines, and the system reaches up to 91% of the theoretical maximum speedup.

## Takeaways
Heterogeneous workloads need heterogeneous speculation — combining pattern-based and learned draft methods accelerates everything without per-workload tuning decisions. Standardized open-source tooling (recipes plus a vLLM plugin) is what makes speculative decoding practical to adopt in production.
