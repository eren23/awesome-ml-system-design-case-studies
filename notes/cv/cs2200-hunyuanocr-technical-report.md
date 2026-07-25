---
id: cs2200
title: HunyuanOCR Technical Report
company: Tencent
primary_category: cv
sub_category: ocr
year: 2025
source_url: https://arxiv.org/abs/2511.19575
tags: [ocr, vlm, end-to-end, document-understanding, xd-rope, multilingual, single-inference-pass, vision-language-model, positional-encoding]
---

# HunyuanOCR Technical Report
**Tencent** · 2025 · [source](https://arxiv.org/abs/2511.19575)

## Problem
OCR systems face a versatility/efficiency trade-off: specialized OCR expert models handle narrow tasks well but lack breadth, while general vision-language models are too heavy for efficient OCR deployment. Traditional cascaded pipelines that depend on preprocessing modules such as layout analysis accumulate errors as each stage's mistakes propagate downstream.

## Approach / System design
Tencent's Hunyuan team built HunyuanOCR, a 1B-parameter OCR-expert VLM using a pure end-to-end paradigm: a native Vision Transformer connected to a lightweight LLM through an MLP adapter, with no preprocessing stages. A single inference pass covers text spotting, document parsing, information extraction, visual question answering, and text-image translation. Training leaned on high-quality data curation at large scale, and reinforcement learning strategies were applied on top of supervised training, which the team reports yielded significant gains on OCR tasks. Production serving runs on vLLM.

## Key decisions
- Unify multiple OCR capabilities in one compact end-to-end model instead of a cascade, eliminating inter-module error propagation.
- Keep the model at 1B parameters to make deployment cheap while still beating much larger general VLMs on OCR workloads.
- Invest in data quality and RL post-training as the main performance levers rather than parameter count.
- Deploy via vLLM for production inference efficiency.

## Stack
Native Vision Transformer + MLP adapter + lightweight LLM (1B parameters total), reinforcement-learning post-training, vLLM-based serving. (The catalog entry additionally notes XD-RoPE positional encoding across text/height/width/time subspaces, 200M+ training image-text pairs, and 130+ language coverage.)

## Results
- Outperforms commercial OCR APIs and larger models such as Qwen3-VL-4B on OCR tasks.
- First place in the ICDAR 2025 DIMT Challenge (Small Model Track).
- State-of-the-art OCRBench results among VLMs under 3B parameters (catalog entry cites OCRBench 860 and OmniDocBench 94.1).

## Takeaways
Commercial-grade OCR doesn't require giant models: a well-trained 1B end-to-end VLM can beat both cascaded expert pipelines and larger general VLMs. Removing pipeline stages removes compounding errors, and RL fine-tuning transfers effectively to OCR objectives. Data quality outweighs scale for domain-expert VLMs.
