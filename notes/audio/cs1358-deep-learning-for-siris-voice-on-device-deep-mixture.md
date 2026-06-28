---
id: cs1358
title: "Deep Learning for Siri's Voice: On-device Deep Mixture Density Networks for Hybrid Unit Selection Synthesis"
company: Apple
primary_category: audio
sub_category: tts
year: 2017
source_url: https://machinelearning.apple.com/research/siri-voices
tags: [tts, on-device, unit-selection, mixture-density-networks, deep-learning]
---

# Deep Learning for Siri's Voice: On-device Deep Mixture Density Networks for Hybrid Unit Selection Synthesis
**Apple** · 2017 · [source](https://machinelearning.apple.com/research/siri-voices)

## Problem
Generate natural, high-quality Siri speech that runs efficiently on-device and improves on traditional unit-selection synthesis.

## Approach / System design
Hybrid unit-selection synthesis: recorded speech is segmented into half-phone units, and the system selects and concatenates units using learned cost functions instead of hand-crafted rules. Deep Mixture Density Networks predict both the target cost and concatenation cost in one framework.

## Key decisions
- Used deep MDNs rather than HMMs to predict target/concatenation costs with uncertainty (variances), enabling context-dependent cost weighting (stable vowels vs. rapid transitions).
- Added a recurrent MDN for fundamental-frequency (f0) modeling to capture utterance-level prosody.
- Used WSOLA for waveform concatenation, plus fast preselection and parallelization for on-device efficiency.

## Stack
3 hidden layers of 512 ReLU units; inputs include quinphone context and syllable/word/phrase features; outputs MFCCs, delta-MFCCs, f0, duration and their predicted variances. Trained on 15–20 hours of 48 kHz studio recordings over a database of 1–2 million half-phone units.

## Results
AB listening tests across 13 language variants showed listeners clearly preferred the new deep-MDN voices, with iOS 10+ preferred over iOS 9 at 50%+ rates.

## Takeaways
Combining probabilistic uncertainty modeling with deep learning yields context-aware cost functions that improve quality, while classic optimizations keep it running on-device.
