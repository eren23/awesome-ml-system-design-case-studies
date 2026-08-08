---
id: cs2422
title: "How Baseten Achieves Better Cost Performance for AI Inference"
company: Baseten
primary_category: genai
sub_category: inference-opt
year: 2025
source_url: https://cloud.google.com/blog/products/ai-machine-learning/how-baseten-achieves-better-cost-performance-for-ai-inference
tags: [inference-optimization, llm-serving, trtllm, gpu-efficiency, cost-performance, google-cloud]
---

# How Baseten Achieves Better Cost Performance for AI Inference
**Baseten** · 2025 · [source](https://cloud.google.com/blog/products/ai-machine-learning/how-baseten-achieves-better-cost-performance-for-ai-inference)

## Problem
Serving large language models at production scale—especially reasoning-heavy models used in agentic workflows—is prohibitively expensive with conventional infrastructure. Baseten needed to make high-throughput LLM inference cost-effective enough to unlock production deployment of models like DeepSeek V3/R1 and Llama 4 for enterprise customers.

## Approach / System design
Baseten pursues a dual strategy: maximizing hardware utilization through the latest NVIDIA GPUs (including A4 VMs with HGX B200 Blackwell chips on Google Cloud) while coupling that hardware with a carefully tuned open-source software stack. On the software side, Baseten uses TensorRT-LLM, NVIDIA Dynamo, SGLang, and vLLM, applying techniques such as kernel fusion, memory hierarchy optimization, and custom attention kernels. For resilience, the platform runs across multiple clouds and regions, using Google Cloud's Dynamic Workload Scheduler for automated failover and workload migration.

## Key decisions
Choosing the open-source inference ecosystem (TensorRT-LLM, Dynamo, vLLM, SGLang) rather than building proprietary inference software gives Baseten flexibility and access to rapidly improving community optimizations. Adopting Blackwell-generation GPUs rather than staying on older silicon was a deliberate bet on hardware-software co-optimization to achieve step-change throughput improvements. Multi-cloud architecture with automated failover prevents single-cloud outages from affecting customers.

## Stack
NVIDIA GPUs (T4 through A4/HGX B200), TensorRT-LLM, NVIDIA Dynamo, SGLang, vLLM, Google Cloud AI Hypercomputer, Dynamic Workload Scheduler, Google Cloud Marketplace.

## Results
Baseten achieved 225% better cost-performance for high-throughput inference workloads (DeepSeek V3, DeepSeek R1, Llama 4) and 25% better cost-performance for latency-sensitive inference on Google Cloud infrastructure. For Writer's Palmyra LLMs specifically, TensorRT-LLM optimization delivered a 60% throughput improvement. The platform ranked first on OpenRouter's LLM performance leaderboard.

## Takeaways
Inference cost-performance is determined as much by software optimization as by hardware choice—combining the latest GPUs with kernel-level tuning and purpose-built inference frameworks is necessary to close the gap. Multi-cloud scheduling with automatic failover turns resilience from an operational burden into a competitive feature for inference infrastructure providers.
