---
id: cs2374
title: "Introducing MAI-Transcribe-1, MAI-Voice-1, and MAI-Image-2 in Microsoft Foundry"
company: Microsoft
primary_category: audio
sub_category: asr
year: 2025
source_url: https://techcommunity.microsoft.com/blog/azure-ai-foundry-blog/introducing-mai-transcribe-1-mai-voice-1-and-mai-image-2-in-microsoft-foundry/4507787
tags: [asr, tts, multilingual, enterprise-speech, azure, speech-foundry, low-cost-inference, voice-generation]
---

# Introducing MAI-Transcribe-1, MAI-Voice-1, and MAI-Image-2 in Microsoft Foundry
**Microsoft** · 2025 · [source](https://techcommunity.microsoft.com/blog/azure-ai-foundry-blog/introducing-mai-transcribe-1-mai-voice-1-and-mai-image-2-in-microsoft-foundry/4507787)

## Problem
Voice is becoming the primary interface for AI agents, and building good voice experiences requires models that can both listen and speak with precision — at a GPU cost that makes enterprise-scale deployment predictable. Microsoft wanted a first-party audio AI stack in Foundry rather than relying on third-party speech models.

## Approach / System design
Microsoft AI released three models into public preview on Microsoft Foundry:
- **MAI-Transcribe-1**: first-generation speech recognition supporting up to 25 languages, engineered for enterprise-grade reliability across accents and real-world audio conditions.
- **MAI-Voice-1**: high-fidelity speech generation producing 60 seconds of expressive audio in under one second on a single GPU.
- **MAI-Image-2**: their highest-capability text-to-image model (debuted top-3 on the Arena.ai leaderboard for image model families).
The speech models are exposed through Azure Speech alongside its 700+ voice gallery; a MAI Playground lets developers test by speaking, recording, or uploading audio. The same models already power Copilot (Voice Mode transcription, dictation, Audio Expressions, podcast features), Bing, PowerPoint, and Azure Speech. Custom voice cloning via MAI-Voice-1 works through Azure Speech's Personal Voice feature from a 10-second sample, gated by a responsible-AI approval process.

## Key decisions
- Compete on inference efficiency: MAI-Transcribe-1 targets competitive accuracy at roughly 50% lower GPU cost than leading transcription alternatives, translating to more predictable enterprise pricing.
- Dogfood first: ship the same models already running Microsoft's own products, then expose them exclusively through Foundry.
- Ship listening and speaking as a paired first-party stack for end-to-end voice agent experiences (IVR, agent assist, live captioning, subtitling, education, market insights).
- Gate voice cloning behind an approval process consistent with responsible-AI policies.

## Stack
Microsoft Foundry, Azure Speech (deployment surface, 700+ voice gallery, Personal Voice), MAI Playground; single-GPU inference for MAI-Voice-1. Model architectures are not disclosed.

## Results
- MAI-Transcribe-1: enterprise-grade accuracy across 25 languages at ~50% lower GPU cost than leading alternatives; priced from $0.36/hour.
- MAI-Voice-1: 60 seconds of expressive audio generated in under 1 second on one GPU; priced from $22 per 1M characters.
- MAI-Image-2: debuted #3 among text-to-image model families on the Arena.ai leaderboard; from $5 per 1M text input tokens; WPP among first enterprise partners using it for creative production.

## Takeaways
Speech AI competition is shifting from raw accuracy to cost-efficiency per GPU-hour — near-parity accuracy at half the serving cost is the pitch enterprises respond to. Proving models inside your own high-volume products (Copilot, Bing) before external release both de-risks the launch and serves as the marketing, and pairing ASR with fast TTS as one platform stack targets the emerging voice-agent workload directly.
