---
id: cs1359
title: On-device Neural Speech Synthesis
company: Apple
primary_category: audio
sub_category: tts
year: 2021
source_url: https://machinelearning.apple.com/research/on-device-neural-speech
tags: [tts, on-device, tacotron, wavernn, model-optimization, mobile]
---

# On-device Neural Speech Synthesis
**Apple** · 2021 · [source](https://machinelearning.apple.com/research/on-device-neural-speech)

## Problem
Neural TTS like Tacotron + WaveRNN sounds natural but is computationally expensive and can be brittle, making it hard to deploy on mobile devices.

## Approach / System design
A fully neural pipeline: grapheme/phoneme input goes to a Mel-spectrogram intermediate, which is then converted directly to speech samples. The work targets both server and mobile deployment, emphasizing modeling and optimization improvements over a new architecture.

## Key decisions
- Prioritized optimization strategies and modeling tweaks rather than redesigning the architecture.
- Treated mobile-device constraints as a primary design target.
- Aimed to keep quality near natural speech while cutting compute.

## Stack
Tacotron (acoustic model), WaveRNN (vocoder), Mel-spectrogram intermediate features, 24 kHz output.

## Results
Generates high-quality 24 kHz speech at roughly 5x faster than real time on server and 3x faster than real time on mobile.

## Takeaways
With targeted optimization, fully neural TTS is practical on-device, and quality need not be sacrificed for deployment efficiency across heterogeneous hardware.
