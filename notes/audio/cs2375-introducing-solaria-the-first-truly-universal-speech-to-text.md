---
id: cs2375
title: "Introducing Solaria, the first truly universal speech-to-text model"
company: Gladia
primary_category: audio
sub_category: asr
year: 2024
source_url: https://www.gladia.io/blog/introducing-solaria-the-first-truly-universal-speech-to-text-model
tags: [speech-to-text, multilingual, universal-model, low-latency, real-time-transcription, whisper, Solaria]
---

# Introducing Solaria, the first truly universal speech-to-text model
**Gladia** · 2024 · [source](https://www.gladia.io/blog/introducing-solaria-the-first-truly-universal-speech-to-text-model)

## Problem
Voice AI platforms, multilingual customer support, and enterprise transcription needed speech-to-text spanning 100+ languages without giving up accuracy or the sub-second latency that natural real-time conversation requires. Many widely spoken languages were simply unsupported by existing STT providers.

## Approach / System design
Gladia built Solaria-1 as a multilingual foundational STT model optimized jointly for accuracy and speed. It serves two modes: real-time streaming for voice agents and live customer interactions, and asynchronous transcription for recordings and long-form audio. Enterprise adaptation is built in — custom vocabulary, named entity recognition, and tunable language sensitivity for domain-specific terminology — with real-time code-switching across languages. Deployment is multi-region (EU/US) with GDPR/HIPAA compliance and SOC 2 certification, and the model integrates with voice-agent frameworks like LiveKit and Daily/Pipecat.

## Key decisions
- Breadth as differentiator: support 100 languages, including 42 not covered by competitors (e.g., Bengali, Punjabi, Tamil, Hebrew, Georgian).
- Prioritize sub-300ms responsiveness so voice agents can handle interruptions and keep conversational flow.
- Ship enterprise customization (custom vocabulary, NER, language sensitivity) rather than a fixed general model.
- Infrastructure-first posture: regional deployment and compliance certifications as core product features.

## Stack
Multilingual deep learning STT model; real-time streaming plus async processing pipelines; LiveKit and Daily/Pipecat integrations; EU/US infrastructure with SOC 2, GDPR, and HIPAA compliance. (Per the catalog metadata, the model was reengineered from Whisper.)

## Results
- 94% Word Accuracy Rate in English, versus 93.5% for Deepgram and 91.5% for AssemblyAI in Gladia's comparison.
- 270ms time-to-first-byte on interrupts; ~698ms latency on final transcript delivery.
- 100+ languages supported with real-time code-switching.

## Takeaways
Competitive STT is a three-way balance of speed, accuracy, and linguistic coverage — winning underserved languages while holding sub-300ms latency is what enables truly global real-time voice products. Enterprise adoption additionally hinges on customization hooks and compliance-ready infrastructure, not just model quality.
