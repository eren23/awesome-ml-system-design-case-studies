---
id: cs1025
title: Advancing Speech Accessibility with Personal Voice
company: Apple
primary_category: audio
sub_category: asr
year: 2023
source_url: https://machinelearning.apple.com/research/personal-voice
tags: [product feature]
---

# Advancing Speech Accessibility with Personal Voice
**Apple** · 2023 · [source](https://machinelearning.apple.com/research/personal-voice)

## Problem
Let people at risk of losing the ability to speak (e.g., ALS or other progressive conditions) preserve their own voice and use it for real-time communication — while keeping all personal voice data private.

## Approach / System design
A three-stage on-device pipeline: the user records ~150 sentences on-device, the model fine-tunes locally overnight, and the resulting voice drives the "Live Speech" text-to-speech feature for day-to-day communication. All processing stays on the device for privacy.

## Key decisions
- Fine-tune both the acoustic model and the vocoder, not just the acoustic model (worth ~+0.43 MOS).
- Replaced the transformer decoder with dilated convolutions for faster training/inference and lower memory.
- Applied speech augmentation/enhancement to cope with noisy real-world home recordings.
- Used bfloat16 with fp32 accumulation for vocoder fine-tuning.

## Stack
Acoustic model: modified FastSpeech2 with speaker-ID conditioning. Vocoder: WaveRNN-based, fully fine-tuned. Enhancement: U-Net for Mel-spectrum augmentation plus CarGAN for audio recovery. Pretrained on Open SLR LibriTTS (~300 hours, 1000 speakers).

## Results
Voice-quality MOS 3.68 vs. 3.85 for the original recordings; voice-similarity score 3.8 ("close to somewhat same"); speech enhancement added about +0.25 MOS.

## Takeaways
On-device fine-tuning makes a privacy-preserving assistive voice feature practical; speaker adaptation and cleaning up noisy enrollment recordings are key to naturalness.
