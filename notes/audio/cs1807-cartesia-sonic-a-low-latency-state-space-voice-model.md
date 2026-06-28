---
id: cs1807
title: "Cartesia — Sonic: A Low-Latency State Space Voice Model for Lifelike Speech"
company: Cartesia
primary_category: audio
sub_category: audio-classification
year: 2024
source_url: https://cartesia.ai/blog/sonic
tags: [tts, state-space-models, low-latency, streaming, custom-inference-stack]
---

# Cartesia — Sonic: A Low-Latency State Space Voice Model for Lifelike Speech
**Cartesia** · 2024 · [source](https://cartesia.ai/blog/sonic)

## Problem
Real-time conversational AI needs low latency and high efficiency, but transformer models are slow and expensive and struggle to continuously process long multimodal streams on-device.

## Approach / System design
Build Sonic on state space models (SSMs) as the core architecture for an efficient, streaming-native voice model, starting with speech generation and a custom-built inference stack tuned for SSM execution. The product exposes a low-latency API with instant voice cloning and voice-design controls, plus a web playground.

## Key decisions
- Chose SSMs over transformers for inherent efficiency on long streaming sequences.
- Built an in-house inference stack specialized for SSMs rather than reusing transformer tooling.
- Optimized for low latency, not just output quality.

## Stack
State space models (S4/Mamba-style), a custom inference stack, trained on Multilingual LibriSpeech, served via a low-latency API and web playground.

## Results
Versus parameter-matched transformers: 20% lower validation perplexity, 2x lower downstream word error rate, +1 NISQA quality point (of 5), 1.5x lower time-to-first-audio, 2x faster real-time factor, and 4x higher throughput; model latency about 135 ms.

## Takeaways
A different core architecture (SSMs) can improve latency, quality, cost, and throughput at the same time, making real-time, potentially on-device voice AI more attainable.
