---
id: cs2241
title: Scaling Rufus with 80,000+ AWS Inferentia and Trainium Chips for Prime Day
company: Amazon
primary_category: genai
sub_category: copilots
year: 2024
source_url: https://aws.amazon.com/blogs/machine-learning/scaling-rufus-the-amazon-generative-ai-powered-conversational-shopping-assistant-with-over-80000-aws-inferentia-and-aws-trainium-chips-for-prime-day/
tags: [rufus, inferentia, trainium, inference-scaling, prime-day, hardware-acceleration]
---

# Scaling Rufus with 80,000+ AWS Inferentia and Trainium Chips for Prime Day
**Amazon** · 2024 · [source](https://aws.amazon.com/blogs/machine-learning/scaling-rufus-the-amazon-generative-ai-powered-conversational-shopping-assistant-with-over-80000-aws-inferentia-and-aws-trainium-chips-for-prime-day/)

## Problem
Rufus, Amazon's multi-billion-parameter conversational shopping assistant, had to serve Prime Day traffic: billions of requests at sub-second latency, globally, on infrastructure that stayed low-cost, performant, and highly available.

## Approach / System design
Rufus ran across three AWS Regions on a heterogeneous fleet of Inferentia2 and Trainium instances. A RAG system enriches responses with product data. A custom traffic orchestrator built on CloudWatch metrics re-routes requests across regions in under 15 minutes as traffic patterns shift. Serving uses NVIDIA Triton Inference Server with a Python backend running vLLM, containerized on Amazon ECS behind Application Load Balancers; multiple services aggregate responses in real time over gRPC, and tokens stream to users as they're generated rather than waiting for the full response.

## Key decisions
- Purpose-built accelerators (Inferentia2 + Trainium) with a single unified configuration via the AWS Neuron SDK — only tensor parallelism differed (24 on Inf2, 32 on Trn1).
- Least-outstanding-requests (LOR) load balancing, which improved throughput five-fold versus the baseline routing.
- Continuous batching via vLLM with prefill prioritized, keeping time-to-first-token low under heavy concurrency.
- INT8 weight-only quantization and Neuron-compiler memory-bandwidth optimization.

## Stack
AWS Inferentia2 and Trainium, AWS Neuron SDK, NVIDIA Triton Inference Server (Python backend), vLLM, PyTorch Lightning, Amazon ECS, Application Load Balancer, Amazon CloudWatch, gRPC, multi-region AWS deployment.

## Results
Over 80,000 Inferentia and Trainium chips served Prime Day, averaging 3 million tokens per minute with P99 time-to-first-response under 1 second. The chips delivered 4.5x lower cost than evaluated alternatives and 54% better performance-per-watt; Trn1 gave a further ~20% latency/throughput improvement over Inf2.

## Takeaways
Purpose-built accelerators change LLM serving economics at extreme scale. Continuous batching is what preserves latency under peak concurrency, multi-region operation demands automated traffic orchestration, and the wins came from co-optimizing the whole stack — inference framework (vLLM), hardware SDK (Neuron), and serving platform (Triton) — rather than any single layer.
