---
id: cs2185
title: Distributed Self-Distillation for Large-Scale ASR Training
company: Speechmatics
primary_category: audio
sub_category: asr
year: 2025
source_url: https://blog.speechmatics.com/distirbuted-self-distillation
tags: [self-distillation, EMA, distributed-training, DDP, FSDP, ASR, training-efficiency]
---

# Distributed Self-Distillation for Large-Scale ASR Training
**Speechmatics** · 2025 · [source](https://blog.speechmatics.com/distirbuted-self-distillation)

## Problem
Self-distillation training (for ASR pretraining) runs two networks at once: a student updated by backpropagation and a teacher updated as an exponential moving average (EMA) of the student. Naively distributing this across GPUs wastes memory by fully replicating both networks and adds redundant computation and communication.

## Approach / System design
The post walks through three distributed strategies of increasing sophistication: (1) DDP with both student and teacher fully replicated on every GPU; (2) FSDP sharding the student only, with the teacher still replicated; and (3) identically sharding both student and teacher with FSDP. The key insight is that with identical sharding, each GPU's teacher shard depends only on its local student shard, so the EMA update becomes purely local with no communication overhead — the distributed topology is designed around the algorithm's structure rather than forcing the algorithm into standard patterns.

## Key decisions
- Reject teacher replication: the EMA teacher is sharded exactly like the student so EMA updates need no AllGather.
- Match sharding layouts between student and teacher — identical sharding is required for the local EMA update to be correct.
- Mixed precision: BF16 weights with FP32 optimizer states.

## Stack
PyTorch DDP and FSDP (ZeRO-3-style parameter sharding), EMA teacher-student self-distillation, BF16/FP32 mixed precision, H100 GPUs with NVLink.

## Results
Per-GPU memory (P = parameter count, N = GPUs): DDP ≈ 14P bytes; FSDP-student-only ≈ (14/N + 2)P bytes; identical FSDP sharding ≈ 14P/N bytes. Identical sharding also eliminates an ~50ms AllGather overhead per step cited for a 25B-parameter model on NVLink-connected H100s.

## Takeaways
Multi-network training regimes like self-distillation don't fit stock distributed recipes; aligning the sharding topology with the algorithm's dependency structure (student shard → teacher shard) yields both the best memory scaling and zero-communication teacher updates.
