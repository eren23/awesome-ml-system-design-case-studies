---
id: cs2344
title: Robust LLM Training Infrastructure at ByteDance
company: ByteDance
primary_category: mlops
sub_category: platform
year: 2025
source_url: https://arxiv.org/abs/2509.16293
tags: [llm-training, fault-tolerance, gpu-infrastructure, distributed-training, failure-recovery, large-scale]
---

# Robust LLM Training Infrastructure at ByteDance
**ByteDance** · 2025 · [source](https://arxiv.org/abs/2509.16293)

## Problem
At ByteDance's production scale (clusters of 9,600–16,384 GPUs), LLM training fails roughly once every 2.78 hours. A three-month analysis found 38,236 explicit failures (CUDA errors, OOM, network faults) and 5,948 implicit failures (hangs, silent data corruption, MFU degradation) across 778,135 training jobs. Implicit failures lack clear diagnostic signals, identical symptoms can stem from infrastructure or user code, and traditional failover (checkpoint reload, rescheduling) costs hours, crushing the effective training time ratio (ETTR).

## Approach / System design
ByteRobust is ByteDance's GPU cluster management system for LLM training, built on the philosophy of "rapid isolation, not precise localization" — evict suspect machines fast rather than debug root causes exhaustively. Detection runs lightweight second-interval inspection threads over network, GPU, and host health plus training metrics (loss, gradient norm, MFU), catching common errors in seconds. Diagnosis is hierarchical at stop time: standard tests (EUD, NCCL, bitwise alignment), then reattempt for transient faults, then rollback of recent code changes, then dual-phase replay that preserves TP/PP dimensions while varying DP to isolate silent data corruption via group testing. Implicit failures are triaged by capturing process stack traces and aggregating them — healthy ranks cluster into dominant groups, outlier parallel groups are over-evicted. Recovery combines in-place hot-update of code without destroying pod environments, a warm-standby machine pool sized to the P99 simultaneous-failure count, and over-eviction-aware checkpointing: asynchronous per-iteration checkpoints with cross-parallel-group backup shards in CPU memory and local SSD, avoiding remote storage.

## Key decisions
- Coarse-grained over-eviction (accepting 6–7 false-positive machines per decision) over precise root-cause diagnosis, trading hardware for recovery speed.
- Data-driven stack-trace aggregation instead of exhaustive stress testing for implicit failures.
- Lazy application of non-critical code changes at the next failover instead of stopping training.
- Hierarchical checkpoint storage (CPU memory + local SSD) after observing 1,104 HDFS errors from remote-storage dependence.

## Stack
Kubernetes CRDs with ~20k lines of Go for the control plane, gRPC agent communication, Python data-plane daemons per pod with py-spy and flight-recorder stack capture, an event-driven runtime analyzer (~12k lines Go), and dual-buffer CPU-tensor checkpointing (~3k lines Python). Deployed on up to 1,200 machines (9,600 H100 GPUs) in production and evaluated on 16,384 L20 GPUs, running dense 70B+ and MoE 200B+ jobs.

## Results
97% cumulative ETTR on a three-month training job on 9,600 GPUs, with sliding-window ETTR above 95% and a maximum unproductive stretch of 50 minutes. Detection time fell to 10–30 seconds versus 10–30 minute timeout baselines. Hot-update recovery is 11.04x faster than full requeue; warm standby is 10.87x faster than requeue. Checkpointing overhead is 0.71% MFU loss versus ~60% for a blocking approach (99.69% stall reduction). 73% of explicit failures are resolved by automatic eviction plus restart; simple mechanisms (eviction 32.5%, reattempt 22.7%, rollback 9.2%) handle 64.4% of incidents, with only 1.23% needing dual-phase replay. Continuous hot updates improved MFU 1.25–1.58x over initial runs.

## Takeaways
- Simple mechanisms resolve most incidents; reserve expensive diagnosis for the rare remainder.
- Implicit failures are the hidden cost — stack-trace aggregation is a pragmatic triage tool.
- Multi-month training means continuous code evolution; rollback and lazy updates are infrastructure requirements, not conveniences.
- Per-iteration in-memory checkpointing with peer backup is feasible at scale, and remote storage is a liability.
- Vendor diagnostics lag hardware (EUD catches only ~70% of SDC); system-level isolation compensates.
