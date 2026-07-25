---
id: cs2358
title: "Gemini: A Family of Highly Capable Multimodal Models"
company: Google DeepMind
primary_category: rl
sub_category: rlhf
year: 2023
source_url: https://arxiv.org/abs/2312.11805
tags: [rlhf, rlaif, multimodal, llm, alignment, instruction-tuning, gemini, production]
---

# Gemini: A Family of Highly Capable Multimodal Models
**Google DeepMind** · 2023 · [source](https://arxiv.org/abs/2312.11805)

## Problem
Google needed a single family of foundation models with strong joint understanding across image, audio, video, and text, spanning deployment contexts from datacenter-scale reasoning to memory-constrained on-device use — and aligned well enough to ship responsibly across Google products.

## Approach / System design
Gemini is a family of natively multimodal models in three sizes: Ultra for the most complex reasoning tasks, Pro for balanced performance and scalable deployment, and Nano for on-device, memory-constrained applications. The models are trained on multimodal data so cross-modal understanding is built in rather than assembled from separate per-modality encoders. Before production deployment, the models go through post-training alignment stages; per the catalog metadata this includes RLHF-style reinforcement fine-tuning, though the fetched source content does not detail the alignment pipeline.

## Key decisions
- Native multimodality: one model family handles image, audio, video, and text rather than stitching modality-specific systems together.
- A three-tier size ladder (Ultra/Pro/Nano) targeting different capability/latency/memory envelopes from the same family.
- Emphasis on responsible deployment practices as part of the release, alongside capability work.

## Stack
Not covered in the fetched source content (infrastructure details were not in the retrieved material).

## Results
Gemini Ultra advanced the state of the art on 30 of 32 evaluated benchmarks, was the first model to reach human-expert performance on MMLU, and improved the state of the art on every one of the 20 multimodal benchmarks examined.

## Takeaways
Building multimodality into pretraining, rather than bolting modalities together afterward, produced broad state-of-the-art coverage across text and multimodal benchmarks. Sizing the same aligned family for cloud and on-device targets lets one training investment serve very different production surfaces.
