---
id: cs2199
title: Video Invisible Watermarking at Scale
company: Meta
primary_category: cv
sub_category: object-detection
year: 2025
source_url: https://engineering.fb.com/2025/11/04/video-engineering/video-invisible-watermarking-at-scale/
tags: [watermarking, video, ai-generated-detection, content-provenance, cpu-optimization, ffmpeg, pytorch, invisible-watermark, pixel-embedding]
---

# Video Invisible Watermarking at Scale
**Meta** · 2025 · [source](https://engineering.fb.com/2025/11/04/video-engineering/video-invisible-watermarking-at-scale/)

## Problem
Meta needed a way to track video content provenance at platform scale — detecting AI-generated content, identifying first uploaders, and determining creation tools. Metadata tags are stripped by editing and re-encoding, and visible watermarks degrade the viewing experience, so the signal had to live invisibly in the pixels themselves and survive compression.

## Approach / System design
Meta built an ML-based invisible watermarking system as a custom FFmpeg filter that embeds a payload of more than 64 bits frame-by-frame through subtle pixel-value modifications, with PyTorch handling model inference. Rather than migrating to a specialized inference service, the team kept everything inside the existing FFmpeg video-processing pipeline for flexibility. A novel frame-selection strategy limits how many frames are modified to reduce bitrate (BD-Rate) impact while preserving detection accuracy and visual quality. Quality was validated through custom post-processing plus crowdsourced manual inspection, because standard visual-quality scores don't capture watermark-specific artifacts.

## Key decisions
- Abandoned GPU inference for CPU-only deployment: GPU suffered from CPU-GPU transfer overhead on high-resolution frames, latency growth under parallel requests, and model-loading time. After threading and embedding-parameter tuning, single-process CPU end-to-end latency landed within 5% of GPU — and multiple FFmpeg processes could run in parallel on CPUs without latency degradation.
- Introduced frame selection to cut the initial ~20% BD-Rate (bitrate) regression down substantially while keeping the watermark detectable.
- Rejected VMAF/SSIM as sufficient quality gates; added manual, crowdsourced inspection because traditional metrics miss watermarking-specific perceptual issues.
- Kept the watermarking logic as a reusable FFmpeg filter block so diverse video products can adopt it with minimal customization.

## Stack
FFmpeg (custom filter), PyTorch inference, CPU-only serving with tuned threading across decoder/encoder/model, VideoSeal as the reference state-of-the-art ML watermarking model, load testing against GPU baselines.

## Results
- Final CPU pipeline within 5% of GPU latency (initially CPU was more than 2x slower), at much lower cost and with parallel-process scaling.
- Initial ~20% bitrate regression from watermarking largely eliminated via frame selection and encoding optimizations.
- Payload capacity above 64 bits; deployed across Meta platforms for AI-content detection, first-posting verification, and origin tracing.

## Takeaways
Properly optimized CPU pipelines can match GPU performance for small-model, high-parallelism video workloads at far lower cost. Academic watermarking techniques need substantial production adaptation — compression interactions and bitrate budgets dominate real-world feasibility. Standard video quality metrics are insufficient for invisible watermarking; human inspection remains necessary.
