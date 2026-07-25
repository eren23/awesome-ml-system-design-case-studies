---
id: cs2103
title: Improved End-of-Turn Model Cuts Voice AI Interruptions 39%
company: LiveKit
primary_category: audio
sub_category: asr
year: 2025
source_url: https://blog.livekit.io/improved-end-of-turn-model-cuts-voice-ai-interruptions-39/
tags: [end-of-turn, transformer, multilingual, turn-detection, false-positive-reduction]
---

# Improved End-of-Turn Model Cuts Voice AI Interruptions 39%
**LiveKit** · 2025 · [source](https://blog.livekit.io/improved-end-of-turn-model-cuts-voice-ai-interruptions-39/)

## Problem
Judging when a person has finished speaking requires the cues humans use — semantic content, dialogue context, and prosodic delivery — evaluated in real time. Getting it wrong either interrupts users mid-thought (false positives) or leaves dead air. LiveKit's earlier turn detector still interrupted too often, especially outside English and when users dictated structured content like phone numbers or emails.

## Approach / System design
LiveKit's open-weight turn detector (v0.4.1-intl) is a transformer with an LLM backbone: Qwen2.5-0.5B-Instruct for cheap real-time inference, improved via knowledge distillation from a Qwen2.5-7B teacher to transfer stronger multilingual generalization without increasing latency. Training data was expanded with real call-center transcripts and synthetic dialogues, extra coverage of structured inputs (emails, phone numbers, addresses, credit-card numbers), and deliberately varied STT output formats so the model is robust to whichever speech-to-text provider feeds it. The Qwen base model's multilingual pre-training provides cross-language transfer across the supported languages.

## Key decisions
- Use a small instruct LLM (0.5B) as the runtime model and distill from a 7B teacher — quality of a bigger model at small-model latency.
- Make the model STT-format-agnostic through training-data variation instead of coupling to one transcription provider.
- Consolidate on the multilingual model for all use cases and deprecate the English-only variant.
- Keep weights open for the voice-agent developer community.

## Stack
Qwen2.5-0.5B-Instruct student / Qwen2.5-7B teacher distillation; transformer end-of-turn classifier consuming STT transcripts; shipped as part of LiveKit's voice agent framework.

## Results
- 39.23% relative reduction in false-positive interruptions vs v0.3.0-intl across all tested languages.
- Overall error rate dropped from 18.66% to 11.34%.
- Per-language relative gains ranged from 21.69% (English) to 54.33% (Dutch); generalizes across 14 languages.

## Takeaways
- Distilling a large multilingual LLM into a 0.5B student is an effective recipe for real-time conversational models with tight latency budgets.
- Robustness to messy real inputs (structured dictation, varied STT formats) is where practical turn-detection gains live.
- A single multilingual model beat maintaining per-language variants — simpler to operate and better for non-English users.
