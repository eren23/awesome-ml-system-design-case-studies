---
id: cs2187
title: Using a Transformer to Improve End-of-Turn Detection
company: LiveKit
primary_category: audio
sub_category: asr
year: 2024
source_url: https://blog.livekit.io/using-a-transformer-to-improve-end-of-turn-detection
tags: [end-of-turn, turn-detection, knowledge-distillation, voice-AI, transformer, multilingual, voice-agents]
---

# Using a Transformer to Improve End-of-Turn Detection
**LiveKit** · 2024 · [source](https://blog.livekit.io/using-a-transformer-to-improve-end-of-turn-detection)

## Problem
Voice agents relying on VAD silence timeouts for end-of-turn detection either interrupt users who pause mid-thought or feel sluggish. Silence-based detection has no semantics — it would treat "I understand your point, but…" as a finished turn even though the user clearly intends to continue.

## Approach / System design
LiveKit built a hybrid system pairing acoustic VAD with a semantic model. A small transformer — SmolLM v2 fine-tuned as an End of Utterance (EOU) model — reads the transcribed conversation (the last four turns) and predicts whether the user is done speaking, then dynamically adjusts the VAD silence timeout rather than replacing VAD outright. It slots into the standard STT → LLM → TTS agent pipeline and ships as an open-source LiveKit Agents plugin enabled via a single constructor kwarg on VoicePipelineAgent.

## Key decisions
- Augment VAD (Silero, default 500ms `min_endpointing_delay`) with semantics instead of replacing it.
- Use a small 135M-parameter transformer so inference runs in real time on CPU.
- Limit context to the last four conversation turns for prediction.
- One-kwarg integration to keep adoption friction near zero.

## Stack
SmolLM v2 (HuggingFace) fine-tuned as the EOU model, Silero VAD, LiveKit Agents framework (open-source plugin), CPU inference.

## Results
85% reduction in unintentional interruptions; falsely predicts turn continuation only 3% of the time; ~50ms model inference.

## Takeaways
Semantic-aware turn detection markedly improves conversational naturalness without hurting responsiveness, and a tiny fine-tuned LLM is enough. Flagged future work: multilingual support, audio-native models for multimodal stacks, and paralinguistic cues such as intonation and cadence.
