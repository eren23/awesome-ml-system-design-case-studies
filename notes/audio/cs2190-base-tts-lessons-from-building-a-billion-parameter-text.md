---
id: cs2190
title: "BASE TTS: Lessons from Building a Billion-Parameter Text-to-Speech Model on 100K Hours of Data"
company: Amazon
primary_category: audio
sub_category: tts
year: 2024
source_url: https://www.amazon.science/publications/base-tts-lessons-from-building-a-billion-parameter-text-to-speech-model-on-100k-hours-of-data
tags: [TTS, large-scale, autoregressive-transformer, speechcodes, tokenization, speaker-disentanglement, emergent-prosody, streaming]
---

# BASE TTS: Lessons from Building a Billion-Parameter Text-to-Speech Model on 100K Hours of Data
**Amazon** · 2024 · [source](https://www.amazon.science/publications/base-tts-lessons-from-building-a-billion-parameter-text-to-speech-model-on-100k-hours-of-data)

## Problem
Achieving state-of-the-art speech naturalness at scale, especially on textually complex sentences (compound nouns, emotions, foreign words, punctuation-heavy text) where prior TTS models struggled.

## Approach / System design
BASE TTS is described as the largest TTS model to date: a 1-billion-parameter autoregressive Transformer trained on 100K hours of public-domain speech. It converts raw text into discrete "speechcodes" — a novel speech tokenization — and a convolution-based decoder then generates waveforms incrementally, making output streamable for real-time use.

## Key decisions
- Novel speechcode tokenization with speaker-ID disentanglement and byte-pair-encoding compression, keeping the token sequence compact and speaker-independent.
- Autoregressive Transformer for text-to-speechcodes plus a lightweight convolutional decoder for streamable waveform generation.
- Deliberate study of emergent abilities: probing what prosodic capabilities appear as data passes 10K+ hours and parameters pass 500M+, with purpose-built evaluation sets to measure them.

## Stack
Autoregressive Transformer encoder, convolution-based streaming decoder, discrete speechcodes representation with speaker disentanglement and BPE; benchmarked against YourTTS, Bark, and TortoiseTTS on naturalness.

## Results
Trained at 100K hours / ~1B parameters and evaluated against publicly available large-scale TTS baselines with naturalness as the primary metric; the paper reports emergent prosody capabilities appearing beyond the ~500M-parameter scale. Specific metric values are not covered in the source page.

## Takeaways
Scaling laws familiar from LLMs carry over to speech: large TTS models exhibit emergent prosodic abilities as data and parameters grow. Measuring these capabilities requires specialized evaluation datasets rather than standard naturalness tests alone.
