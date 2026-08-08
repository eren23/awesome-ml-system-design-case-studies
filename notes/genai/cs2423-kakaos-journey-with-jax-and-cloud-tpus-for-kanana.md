---
id: cs2423
title: "Kakao's Journey with JAX and Cloud TPUs for Kanana LLM Pre-Training"
company: Kakao
primary_category: genai
sub_category: fine-tuning
year: 2025
source_url: https://cloud.google.com/blog/products/infrastructure-modernization/kakaos-journey-with-jax-and-cloud-tpus
tags: [llm-pretraining, tpu, jax, maxtext, distributed-training, kanana]
---

# Kakao's Journey with JAX and Cloud TPUs for Kanana LLM Pre-Training
**Kakao** · 2025 · [source](https://cloud.google.com/blog/products/infrastructure-modernization/kakaos-journey-with-jax-and-cloud-tpus)

## Problem
Kakao (operator of KakaoTalk, used by 93% of South Korea's population) hit capacity limits on its GPU-based training infrastructure in terms of both power and budget. The team needed a cost-effective, scalable path to train the Kanana family of Korean-first LLMs at sizes up to 9.8B parameters plus mixture-of-experts variants.

## Approach / System design
Kakao migrated pre-training to JAX on Google Cloud TPUs using MaxText as the primary training framework, supported by Flax for model definition, Optax for optimization, Orbax for checkpointing, and Grain for deterministic data loading. Cluster management is handled through XPK on GKE. To fit their multi-source training data needs, the team extended MaxText's Grain pipeline to support configuration-driven multi-source blending with dynamic weight ratios across training phases. Token processing was also modified to append the first token of each subsequent sequence to the current sequence, creating overlapping boundaries that maximize data utilization and match the behavior of their existing Megatron-LM GPU pipeline for reproducibility.

## Key decisions
JAX was chosen over CUDA-based alternatives for its flexibility in expressing custom training logic and its efficient SPMD and FSDP support on TPU hardware. Using Grain for data loading was prioritized specifically for its deterministic behavior, which is essential for debugging and reproducing results in multi-week training runs. A 2.7x throughput improvement was observed when upgrading from v5e to Trillium TPUs, requiring only configuration changes rather than code rewrites.

## Stack
JAX, MaxText, Flax, Optax, Orbax, Grain, XPK, GKE, Google Cloud TPUs (v5e → Trillium), Megablocks MoE kernels, FSDP.

## Results
Kanana 2.1B trained from scratch on TPUs reproduced GPU (Megatron-LM) benchmark performance at each training stage, validating the infrastructure migration. A depth-upscaled 9.8B model (from an 8B base) showed consistent benchmark improvements. A mixture-of-experts model upcycled from the 2.1B dense model to 13.4B parameters (2.3B active, 64 experts) showed particular gains on code and math benchmarks. Upgrading from v5e to Trillium TPUs delivered a 2.7x throughput increase across all model sizes.

## Takeaways
Investing upfront in a JAX/MaxText stack that can be customized at the Python level—rather than working around a more opaque CUDA framework—paid off in the ability to implement novel data blending strategies and MoE architectures with minimal code changes. Hardware upgrades on TPUs can yield step-change throughput improvements through simple configuration changes, making the cost-performance trajectory favorable compared to GPU capacity expansion.
