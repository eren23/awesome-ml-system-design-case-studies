---
id: cs2099
title: Introducing 3.5x Smaller Voice Isolation Model with Exceptional Accuracy
company: Krisp
primary_category: audio
sub_category: audio-classification
year: 2025
source_url: https://krisp.ai/blog/small-voice-isolation-model/
tags: [speech-enhancement, noise-suppression, model-compression, on-device, telephony]
---

# Introducing 3.5x Smaller Voice Isolation Model with Exceptional Accuracy
**Krisp** · 2025 · [source](https://krisp.ai/blog/small-voice-isolation-model/)

## Problem
Voice AI agents and telephony systems need noise suppression / voice isolation, but full-size models consume too much CPU for edge devices and drive up cost in massive server-side deployments. Krisp needed a much smaller model that kept quality close to its flagship.

## Approach / System design
krisp-viva-tel-lite-v1 is a compressed voice isolation model 3.5x smaller than krisp-viva-tel-v1, optimized for telephony. It processes 16 kHz-bandwidth audio with 15 ms algorithmic latency and supports common telephony codecs (G.729, G.711, G.722, Opus), covering both outbound and inbound call scenarios. Primary-speaker identification uses speaker-to-microphone proximity cues, and performance is maintained on Bluetooth devices such as AirPods. Quality was validated with POLQA (an objective perceived-audio-quality standard) across 72 English files at 10 dB SNR plus narrowband and codec-degraded test sets.

## Key decisions
- Trade a small quality margin in extreme noise for a 3.5x size reduction, keeping the full-size model available for the hardest conditions.
- Target telephony explicitly: codec support and narrowband robustness as first-class requirements.
- Keep latency at 15 ms so the lite model drops into real-time pipelines unchanged.
- Evaluate with POLQA rather than only subjective listening.

## Stack
Krisp VIVA SDK model family (krisp-viva-tel-lite-v1, alongside krisp-viva-tel-v1 and earlier krisp-bvc models); telephony codec integrations; edge/on-device and server-side deployment targets.

## Results
- 3.5x smaller than the predecessor with comparable CPU footprint per unit of capability and 15 ms latency.
- POLQA quality: +2% over the prior lite model on outbound; +5% over krisp-bvc-o-lite-v2 and +8% over krisp-bvc-o-v2 on inbound.
- Per the catalog summary: processing under 20 ms, ~3.5x turn-taking accuracy boost downstream, and ~50% reduction in dropped calls in telephony deployments.

## Takeaways
- Model compression is a product feature: a 3.5x smaller model unlocks edge deployment and cuts serving cost at fleet scale.
- Downstream effects matter — cleaner isolated audio measurably improves turn-taking and call reliability, not just perceived audio quality.
- Keeping a big/small model pair lets customers choose between extreme-noise robustness and footprint.
