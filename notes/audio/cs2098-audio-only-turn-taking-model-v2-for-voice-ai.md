---
id: cs2098
title: Audio-Only Turn-Taking Model v2 for Voice AI — VIVA SDK
company: Krisp
primary_category: audio
sub_category: audio-classification
year: 2025
source_url: https://krisp.ai/blog/krisp-turn-taking-v2-voice-ai-viva-sdk/
tags: [turn-detection, audio-only, voice-agents, end-of-turn, VIVA-SDK]
---

# Audio-Only Turn-Taking Model v2 for Voice AI — VIVA SDK
**Krisp** · 2025 · [source](https://krisp.ai/blog/krisp-turn-taking-v2-voice-ai-viva-sdk/)

## Problem
Voice AI agents need to know when a speaker has actually finished talking. Poor end-of-turn detection makes bots interrupt users or leave awkward gaps, and real-world noisy audio makes the problem much harder than clean benchmark conditions.

## Approach / System design
Krisp's Turn-Taking Model v2 is an audio-only model that predicts end-of-turn in real time from the acoustic signal (no transcript dependency). Relative to v1, the gains come from data rather than architecture novelty: more diverse and better-structured training datasets plus richer augmentations (including noise) to match production conditions. The model ships inside the VIVA SDK (Voice Infrastructure for Voice AI) and is designed to run in a tight pipeline with Krisp's Voice Isolation model (krisp-viva-tel-v2) and VAD, so noise removal feeds cleaner audio into turn detection.

## Key decisions
- Stay audio-only for low latency and independence from any STT provider.
- Invest in training-data diversity and noise augmentation as the main lever for real-world robustness.
- Package Voice Isolation + Turn-Taking + VAD as one integrated pipeline in a single SDK rather than separate components developers must stitch together.

## Stack
Krisp VIVA SDK; audio-only end-of-turn model; paired with krisp-viva-tel-v2 voice isolation and VAD components.

## Results
- Clean audio (~1,800 samples): F1 0.813 (v2) vs 0.804 (v1), with faster mean turn-shift prediction at the same false-positive rate.
- Noisy audio (5–15 dB SNR): F1 0.757 vs 0.71 (~6% improvement); balanced accuracy 0.768 vs 0.723.
- With noise removal applied first: F1 0.808 vs 0.775; AUC 0.885 vs 0.854.
- Per the catalog summary, v2 detects 47% more true turn-shifts within 200ms compared to v1.

## Takeaways
- In turn-taking, data diversity and augmentation drive production gains more than architectural changes.
- Robustness under noise is the differentiator — clean-audio metrics barely moved while noisy-audio metrics improved substantially.
- Co-designing turn detection with noise suppression in one pipeline compounds the benefits of each component.
