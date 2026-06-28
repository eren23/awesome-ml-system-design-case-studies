---
id: cs1377
title: Neural TTS Makes Speech Synthesizers More Versatile
company: Amazon (Alexa / Polly)
primary_category: audio
sub_category: tts
year: 2019
source_url: https://www.amazon.science/blog/neural-text-to-speech-makes-speech-synthesizers-much-more-versatile
tags: [tts, neural-tts, speaking-styles, newscaster, production]
---

# Neural TTS Makes Speech Synthesizers More Versatile
**Amazon (Alexa / Polly)** · 2019 · [source](https://www.amazon.science/blog/neural-text-to-speech-makes-speech-synthesizers-much-more-versatile)

## Problem
Produce natural-sounding synthesized speech that can adopt different speaking styles (e.g., a newscaster style) and transfer prosody across voices, using only a few hours of style-specific data rather than recording each voice in each style.

## Approach / System design
Two complementary techniques. Prosody transfer extracts prosodic features (pitch, tempo, volume) at the phoneme level from source speech and applies them to synthesized output, letting a style be replicated across different voices. A universal vocoder is trained on diverse multilingual speakers so a single model can turn spectrograms into natural waveforms without per-speaker vocoders.

## Key decisions
- Used phoneme-level prosodic features rather than raw spectrograms for better generalization, and normalized them so they transfer to unseen voices.
- Fell back to ASR posteriograms when clean transcripts were unavailable.
- Trained one universal vocoder over 74 speakers across 17 languages instead of speaker-specific vocoders.

## Stack
Neural TTS with spectrogram generation, ASR integration for transcript-free cases, a universal neural vocoder, and MUSHRA listening-test evaluation.

## Results
Prosody transfer showed a statistically insignificant difference between the textless and transcript-based systems. The universal vocoder beat speaker-specific baselines on unseen speakers across whispered, sung, and noisy conditions, approaching natural-speech quality in evaluations.

## Takeaways
Abstracting to phoneme-level features plus multilingual training at scale gives large versatility gains, letting one system adapt to new speakers and styles from limited data.
