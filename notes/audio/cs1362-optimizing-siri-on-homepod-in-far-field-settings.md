---
id: cs1362
title: Optimizing Siri on HomePod in Far-Field Settings
company: Apple
primary_category: audio
sub_category: asr
year: 2018
source_url: https://machinelearning.apple.com/research/optimizing-siri-on-homepod-in-far-field-settings
tags: [far-field, beamforming, echo-cancellation, speech-enhancement, homepod]
---

# Optimizing Siri on HomePod in Far-Field Settings
**Apple** · 2018 · [source](https://machinelearning.apple.com/research/optimizing-siri-on-homepod-in-far-field-settings)

## Problem
HomePod must hear voice commands from several meters away while fighting its own loud playback (30–40 dB louder than the user's speech), room reverberation, background noise, and competing talkers — all on a tight power budget.

## Approach / System design
A multichannel, online (low-latency, always-listening) signal-processing pipeline over six microphones: multichannel echo cancellation (linear adaptive filters), DNN-driven residual echo suppression, dereverberation, mask-based noise reduction, competing-talker separation via blind source separation, and deep-learning stream selection guided by the trigger-phrase detector.

## Key decisions
- Online rather than batch processing to avoid latency in always-listening mode.
- Mask-based enhancement: a DNN predicts speech-presence probability to drive Multichannel Wiener Filters.
- Combined unsupervised source separation with supervised stream selection, using the "Hey Siri" detector as a top-down signal.
- Trained DNNs on real HomePod recordings to capture device-specific nonlinearities.

## Stack
DNNs for SPP/mask estimation and stream selection, blind source separation (O(M²)), multichannel Wiener filtering, running on the A8 chip via Apple's Accelerate framework.

## Results
29.0% absolute false-rejection improvement in competing-talker scenarios; word-error-rate improvements of 40% (reverberation), 90% (playback), 74% (noise), and 61% (competing talker); under 15% of a single A8 core at 1.4 GHz.

## Takeaways
Tightly integrating classical DSP with deep learning beats either alone; top-down acoustic knowledge enables stream selection; online adaptation and power constraints drive the architecture.
