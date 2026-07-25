---
id: cs2293
title: Achieving Near-Linear Training Scalability for Pinterest's Foundation Models
company: Pinterest
primary_category: rec
sub_category: feed-ranking
year: 2026
source_url: https://medium.com/pinterest-engineering/achieving-near-linear-training-scalability-for-pinterests-foundation-models-14d4f59fe6f6
tags: [foundation-model, distributed-training, scalability, homefeed, related-pins, pytorch-dcp]
---

# Achieving Near-Linear Training Scalability for Pinterest's Foundation Models
**Pinterest** · 2026 · [source](https://medium.com/pinterest-engineering/achieving-near-linear-training-scalability-for-pinterests-foundation-models-14d4f59fe6f6)

## Problem
Pinterest's recommendation foundation models (powering Home feed and Related Pins) hold ~99% of their parameters in embedding tables, which makes distributed training communication-bound. Early multi-node attempts were catastrophic: adding a second machine made training 5x slower (0.2x scaling). Even after enabling AWS EFA networking, scaling sat at 1.13x on 2 nodes and 1.21x on 4 nodes — three extra nodes bought only 21% more throughput.

## Approach / System design
Profiling showed NCCL communication for distributed embedding lookups consumed 73% of forward-pass time at 2 nodes, so the team attacked the communication layer from several angles: quantizing all-to-all embedding traffic from FP32 to FP8; balancing embedding-table sharding evenly across GPUs; reshaping tables (halving embedding dims, doubling rows) to shrink per-op transfer while preserving capacity; and adopting a 2D parallel topology that partitions the cluster into groups so expensive all-to-all stays intra-node on NVLink while all-reduce runs over inter-node links.

## Key decisions
- Optimize communication topology first — for embedding-heavy models it dominates compute improvements.
- Preserve model capacity during table reshaping instead of trading accuracy for speed.
- Migrate checkpointing from TorchSnapshot to PyTorch Distributed Checkpoint (DCP) for flexible multi-node workflows.
- Add torch.compile for a further 55% single-node gain via kernel fusion.

## Stack
PyTorch 2.1–2.6, TorchRec 1.1, PyTorch Distributed Checkpoint, FBGEMM quantized-communication library, NCCL, AWS EFA, PyTorch Profiler, torch.compile.

## Results
2-node scaling improved from 1.13x to 2.0x; 4-node from 1.21x to 3.9x (97.5% of ideal); 8 nodes reached 7.5x (93.75% of ideal). All-to-all latency dropped from 78ms to 13ms (83%), NCCL payloads shrank 75%, and end-to-end throughput improved 13x versus the pre-EFA baseline, reaching 490k examples/second on 8 nodes.

## Takeaways
You can't optimize what you don't measure — profiling pinpointed the root cause immediately. No single technique got to near-linear scaling; quantization, sharding balance, table reshaping, and topology-aware placement compounded. The effort produced a repeatable scaling playbook now applied across Pinterest's foundation-model family.
