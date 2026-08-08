---
id: cs1823
title: Wispr Flow — Effortless Voice Dictation with Llama on Baseten
company: Wispr
primary_category: audio
sub_category: asr
year: 2024
source_url: https://www.baseten.co/resources/customers/wispr-flow/
tags: [asr, llm, tensorrt-llm, low-latency, inference-serving, hipaa]
---

# Wispr Flow — Effortless Voice Dictation with Llama on Baseten
**Wispr** · 2024 · [source](https://www.baseten.co/resources/customers/wispr-flow/)

## Problem
Wispr Flow needed to deliver real-time voice dictation that felt instantaneous while handling sensitive user speech data under strict compliance requirements. The system had to meet SOC 2 and HIPAA constraints, which ruled out shared multi-tenant inference infrastructure. Achieving sub-700ms p99 end-to-end latency under these conditions required a purpose-built deployment approach.

## Approach / System design
The pipeline pairs a speech recognition model with a fine-tuned Llama model that post-processes and enhances raw transcripts for fluency and formatting. Baseten Chains is used to orchestrate the two-stage inference flow, linking ASR output directly into the LLM step without a separate round-trip. The entire stack runs on dedicated AWS infrastructure provisioned through Baseten, keeping data isolated per compliance requirements.

## Key decisions
Serving on dedicated rather than shared instances was a non-negotiable choice driven by HIPAA data-isolation requirements. TensorRT-LLM was selected to compile and optimize the Llama model for GPU execution, enabling the low-latency targets. Baseten Chains was chosen to minimize orchestration overhead between the ASR and LLM stages.

## Stack
TensorRT-LLM for optimized LLM inference, Baseten Chains for multi-step pipeline orchestration, dedicated AWS GPU instances, a fine-tuned Llama model for transcript enhancement, and a speech recognition model as the first pipeline stage.

## Results
The system achieves sub-700ms p99 end-to-end latency for the full dictation pipeline. Deployment satisfies SOC 2 and HIPAA compliance requirements through dedicated infrastructure isolation.

## Takeaways
Compliance constraints (HIPAA/SOC 2) can force dedicated-instance deployments that, when combined with compiler-level optimizations like TensorRT-LLM, can still achieve aggressive latency targets. Chaining ASR and LLM inference in a single orchestrated pipeline reduces round-trip overhead significantly compared to independent service calls.
