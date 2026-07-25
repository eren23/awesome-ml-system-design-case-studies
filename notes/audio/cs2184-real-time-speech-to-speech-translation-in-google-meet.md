---
id: cs2184
title: Real-Time Speech-to-Speech Translation in Google Meet
company: Google
primary_category: audio
sub_category: audio-classification
year: 2025
source_url: https://research.google/blog/real-time-speech-to-speech-translation/
tags: [speech-translation, s2st, streaming, AudioLM, SpectroStream, google-meet, real-time, low-latency]
---

# Real-Time Speech-to-Speech Translation in Google Meet
**Google** · 2025 · [source](https://research.google/blog/real-time-speech-to-speech-translation/)

## Problem
Traditional speech-to-speech translation cascades (ASR → machine translation → TTS) incur 4–5 second delays, accumulate errors across stages, and lose speaker personalization — too slow and lossy for natural cross-language conversation.

## Approach / System design
Google replaced the three-stage cascade with a single end-to-end streaming model built on the AudioLM framework. A scalable data pipeline converts raw audio into time-synchronized input/output pairs using integrated ASR/TTS with forced alignment. The model itself is transformer-based: a streaming encoder summarizes ~10-second input audio windows, and an autoregressive decoder predicts translated audio directly. Audio is represented as hierarchical 2D RVQ token sets via the SpectroStream codec (about 16 tokens encoding 100ms at high quality), rather than raw waveforms.

## Key decisions
- End-to-end token-level modeling to eliminate cascade error accumulation and cut latency.
- Adjustable lookahead delay (standard 2 seconds) implemented by shifting ground-truth tokens during training, trading a controlled delay for translation quality.
- Per-token loss computation to keep translations accurate.
- Auxiliary text-token output so BLEU can be computed directly for evaluation.
- Hybrid int8/int4 quantization for efficient inference.

## Stack
AudioLM framework, SpectroStream codec (hierarchical RVQ audio tokens), transformer streaming encoder + autoregressive decoder, TensorFlow with XNNPACK optimization, custom TTS generation engine for training-data creation.

## Results
End-to-end delay of about 2 seconds versus 4–5 seconds for prior cascades. Launched in Google Meet and on Pixel 10, initially supporting translation among English, Spanish, German, French, Italian, and Portuguese.

## Takeaways
Streaming end-to-end architectures with time-aligned training data substantially cut both latency and compounding errors versus cascades. Discrete token-based audio representation is the lever that balances audio quality against computational cost, and training-time tricks (shifted targets) give a tunable latency/quality knob.
