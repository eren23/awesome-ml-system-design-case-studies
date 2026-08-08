---
id: cs1819
title: "Music AI (Moises) — Moises Research Innovations 2025: Lightweight and Diffusion-Based Source Separation"
company: Music AI
primary_category: audio
sub_category: asr
year: "2025"
source_url: https://music.ai/blog/research/Moises-Research-Innovations-2025/
tags: [source-separation, band-split-unet, diffusion, encodec, lyric-transcription]
---

# Music AI (Moises) — Moises Research Innovations 2025: Lightweight and Diffusion-Based Source Separation
**Music AI** · 2025 · [source](https://music.ai/blog/research/Moises-Research-Innovations-2025/)

## Problem
State-of-the-art music source separation models such as BS-RoFormer achieve excellent quality but are too parameter-heavy for real-time execution on mobile and embedded devices. Deploying separation in the Moises app at scale required closing the quality gap with those large models using a fraction of the parameters.

## Approach / System design
Moises-Light is a band-split U-Net designed to match BS-RoFormer's separation quality with approximately 13 times fewer parameters, making it viable for real-time and on-device inference. The research also produced LDM-DMX, a latent diffusion model applied to the separation task, and advances in lyric transcription accuracy — all targeted at the capabilities exposed in the Moises production app.

## Key decisions
Band-split processing preserves the frequency-domain structure that music source separation benefits from while the U-Net backbone provides an efficient encoder-decoder hierarchy. Targeting a 13x parameter reduction over the BS-RoFormer reference model was a conscious product decision driven by the latency and memory constraints of mobile deployment.

## Stack
Band-split U-Net (Moises-Light), latent diffusion model (LDM-DMX), EnCodec for audio representation, lyric-transcription pipeline.

## Results
Moises-Light matches BS-RoFormer-class separation quality while using approximately 13 times fewer parameters. No specific signal-to-distortion ratio or latency figures are covered in the source.

## Takeaways
Parameter-efficient architecture design is not just a research concern but a direct product enabler: hitting near-SOTA separation quality with 13x fewer parameters made real-time mobile deployment possible without quality regression visible to users. Combining deterministic and diffusion-based separation models in the same research programme allows different quality-latency operating points to be offered.
