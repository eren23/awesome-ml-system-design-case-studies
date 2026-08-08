---
id: cs1812
title: "NVIDIA — Accelerating Leaderboard-Topping ASR Models 10x with NeMo"
company: NVIDIA
primary_category: audio
sub_category: asr
year: "2024"
source_url: https://developer.nvidia.com/blog/accelerating-leaderboard-topping-asr-models-10x-with-nvidia-nemo/
tags: [asr, inference-optimization, cuda-graphs, rnnt, bfloat16, label-looping]
---

# NVIDIA — Accelerating Leaderboard-Topping ASR Models 10x with NeMo
**NVIDIA** · 2024 · [source](https://developer.nvidia.com/blog/accelerating-leaderboard-topping-asr-models-10x-with-nvidia-nemo/)

## Problem
NeMo ASR models that topped accuracy leaderboards were too slow for cost-effective production inference. Two specific bottlenecks limited throughput: the overhead of casting operations in automatic mixed-precision (AMP) inference, and the per-step kernel-launch latency inside the RNN-T/TDT transducer decoding loop.

## Approach / System design
The team eliminated AMP by running all computations natively in bfloat16, removing the repeated cast operations that AMP injects between layers. For the transducer decoder, they developed a label-looping algorithm that fuses decoding steps and wraps the loop with CUDA Graphs conditional nodes, so the kernel-launch overhead for each decoding step is paid once at graph capture time rather than at every inference call.

## Key decisions
Choosing bfloat16 over float16 was deliberate: bfloat16 matches float32's dynamic range, avoiding the overflow and underflow instability that float16 introduces in speech models while still enabling full-precision casting elimination. Using CUDA Graphs conditional nodes was necessary because transducer decoding has data-dependent branching that earlier versions of CUDA Graphs could not capture.

## Stack
bfloat16 inference, CUDA Graphs with conditional node support, RNN-T and TDT transducer decoders, NVIDIA NeMo framework.

## Results
The combined optimisations achieved a 10x inference speedup over the unoptimised NeMo baseline. No absolute throughput figures are covered in the source.

## Takeaways
Inference efficiency gains of this magnitude often come from eliminating systematic overheads — such as casting and kernel launches — rather than from architectural changes. CUDA Graphs are a powerful tool for amortising kernel-launch costs in iterative decoding loops once the graph framework supports the required control flow.
