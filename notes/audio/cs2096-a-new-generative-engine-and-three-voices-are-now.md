---
id: cs2096
title: A New Generative Engine and Three Voices Are Now Generally Available on Amazon Polly
company: Amazon (AWS)
primary_category: audio
sub_category: tts
year: 2024
source_url: https://aws.amazon.com/blogs/aws/a-new-generative-engine-and-three-voices-are-now-generally-available-on-amazon-polly/
tags: [generative-tts, billion-parameter, BASE-TTS, streamable, amazon-polly]
---

# A New Generative Engine and Three Voices Are Now Generally Available on Amazon Polly
**Amazon (AWS)** · 2024 · [source](https://aws.amazon.com/blogs/aws/a-new-generative-engine-and-three-voices-are-now-generally-available-on-amazon-polly/)

## Problem
Polly's earlier engines had quality ceilings: the 2016 standard engine used concatenative synthesis with inherent naturalness limits, and the 2019 neural engine improved quality but still lacked the expressiveness and emotional range needed for use cases like customer assistance and marketing content.

## Approach / System design
The new generative engine is powered by BASE TTS ("Big Adaptive Streamable TTS with Emergent abilities") — a billion-parameter transformer trained on roughly 100,000 hours of publicly available and proprietary speech data spanning multiple voices, languages, and styles. Text is converted through phoneme processing into spectrograms, and a neural vocoder (with a streamable decoder) renders the continuous audio signal. The scale of the model yields emergent qualities: context-dependent prosody, natural pausing, and dialect handling without explicit rules.

## Key decisions
- Bet on a large generative transformer rather than incremental neural-TTS improvements, trading model size for emergent naturalness.
- Keep the engine streamable so it fits Polly's real-time synthesis use cases.
- Offer the generative engine alongside existing standard, neural, and long-form engines instead of replacing them, letting customers pick a quality/cost point.
- Launch GA in a single region first (US East, N. Virginia).

## Stack
BASE TTS 1B-parameter transformer; phoneme → spectrogram pipeline with neural vocoder / streamable convolution decoder; delivered through the Amazon Polly service via AWS Management Console, CLI, and SDKs (including Java, Python, iOS, Android). Character-count-based pricing.

## Results
Three expressive voices at GA: Ruth and Matthew (US English) and Amy (British English), described as the most human-like and emotionally engaged Polly voices to date. No quantitative quality benchmarks are given in the post.

## Takeaways
- Scaling TTS to billion-parameter generative models trained on ~100K hours produces emergent prosody and naturalness that smaller pipeline systems can't match.
- Productizing research (BASE TTS) as one engine option in an existing managed service lets customers adopt cutting-edge synthesis without migration risk.
