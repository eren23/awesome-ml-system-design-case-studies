---
id: cs2101
title: "Introducing Aura-2: Enterprise-Grade Text-to-Speech"
company: Deepgram
primary_category: audio
sub_category: tts
year: 2025
source_url: https://deepgram.com/learn/introducing-aura-2-enterprise-text-to-speech
tags: [enterprise-TTS, low-latency, Deepgram-Enterprise-Runtime, voice-agents, domain-specific]
---

# Introducing Aura-2: Enterprise-Grade Text-to-Speech
**Deepgram** · 2025 · [source](https://deepgram.com/learn/introducing-aura-2-enterprise-text-to-speech)

## Problem
Most TTS systems are tuned for entertainment (audiobooks, character voices) rather than enterprise workloads. In production voice agents, what matters is real-time responsiveness, correct pronunciation of structured content (drug names, URLs, account numbers, currency, addresses), tone consistency, and scalable/cost-effective serving — areas where expressive consumer TTS falls short.

## Approach / System design
Aura-2 is built on the Deepgram Enterprise Runtime (DER), the same serving infrastructure behind Deepgram's STT and voice-agent products: GPU-accelerated inference with model quantization and pruning, streaming-first synthesis (audio starts before generation finishes), lossless compression on the wire, stateless design for distributed orchestration, hot-swappable model deployment with zero downtime, and flexible hosting (cloud, VPC, on-prem). The model ships 40+ voices designed for enterprise contexts and is trained on real conversational data from domains like healthcare, finance, and customer support; a passive-learning loop lets the runtime adapt to new terminology encountered in live traffic. Sharing a stack with Deepgram STT gives consistent entity handling/pronunciation across the full voice pipeline.

## Key decisions
- Optimize for "boring but correct": neutral prosody, consistency, and structured-data pronunciation over celebrity-style expressiveness.
- Reuse one runtime (DER) across STT, TTS, and voice agents instead of standing up separate serving stacks.
- Train on domain-specific call-center and transactional speech rather than narration corpora.
- Price aggressively for scale.

## Stack
Deepgram Enterprise Runtime; quantized/pruned GPU inference; streaming synthesis; cloud/VPC/on-prem deployment options; unified STT+TTS entity handling.

## Results
- Latency: sub-200ms time-to-first-byte; real-time factor 0.111x (~100ms to synthesize 1s of audio), with minimal variance under load.
- Preference testing (2,794 three-way comparisons, 8,382 samples): ~60% preference for Aura-2 in customer-service scenarios; four of the five most-preferred enterprise voices were Aura-2.
- Pronunciation eval (280+ utterances across currency, dates, emails, URLs, addresses): led Azure, Google, ElevenLabs, PlayHT, Cartesia, and OpenAI on "Good" ratings.
- Pricing: $0.030 per 1,000 characters, under Cartesia Sonic ($0.038) and ElevenLabs Flash ($0.050).

## Takeaways
- Enterprise TTS is a different product from entertainment TTS: pronunciation accuracy, latency, and consistency at scale beat maximal expressiveness.
- A unified STT/TTS runtime pays off in latency, operational simplicity, and pipeline-consistent entity pronunciation.
- Infrastructure work (quantization, streaming, stateless serving) is as central to the offering as the model itself.
