---
id: cs2183
title: "SAM Audio: A Unified Multimodal Model for Audio Separation"
company: Meta
primary_category: audio
sub_category: audio-classification
year: 2025
source_url: https://ai.meta.com/blog/sam-audio/
tags: [audio-separation, multimodal, flow-matching, diffusion-transformer, source-separation, text-prompt, visual-prompt]
---

# SAM Audio: A Unified Multimodal Model for Audio Separation
**Meta** · 2025 · [source](https://ai.meta.com/blog/sam-audio/)

## Problem
Audio separation tooling has been fragmented into single-purpose systems — instrument separation, speech extraction, noise removal — each with its own model. Users lacked one intuitive way to isolate an arbitrary sound from a complex mixture.

## Approach / System design
SAM Audio is a unified, generative separation model prompted multimodally: text prompts ("dog barking"), visual prompts (clicking an object in a video), or span prompts (marking a time segment). A flow-matching diffusion transformer encodes prompts and audio into a shared representation and generates both the target track and the residual. A Perception Encoder Audiovisual (PE-AV) aligns frame-level video features with audio at precise moments so visually-grounded separation is temporally accurate. Training data comes from a data engine combining advanced audio mixing, automated multimodal prompt generation, and pseudo-labeling.

## Key decisions
- Generative flow-matching diffusion transformer rather than mask-based discriminative separation, producing target plus residual tracks.
- Shared prompt/audio representation to unify text, visual, and span prompting in one model.
- PE-AV encoder for tight audio-video temporal alignment.
- Data engine with pseudo-labeling to synthesize realistic separation training data at scale (trained on 100+ million videos).

## Stack
Flow-matching diffusion transformer, PE-AV audiovisual encoder, PyTorchVideo, FAISS, contrastive learning frameworks; released in 500M–3B parameter sizes and deployed in the Segment Anything Playground.

## Results
Runs faster than real time (RTF ≈ 0.7); outperforms prior universal audio-separation models and matches the best domain-specific models across audio categories.

## Takeaways
A single promptable model can replace a zoo of specialized separators once prompts, audio, and video share one representation — bringing professional-grade audio editing to non-experts, in the same spirit as SAM did for image segmentation.
