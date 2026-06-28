---
id: cs1376
title: Amazon Alexa's new wake word research at Interspeech
company: Amazon (Alexa)
primary_category: audio
sub_category: speaker-id
year: 2018
source_url: https://www.amazon.science/blog/amazon-alexas-new-wake-word-research-at-interspeech
tags: [wake-word, cnn, on-device, false-accept, noise-robustness, alexa]
---

# Amazon Alexa's new wake word research at Interspeech
**Amazon (Alexa)** · 2018 · [source](https://www.amazon.science/blog/amazon-alexas-new-wake-word-research-at-interspeech)

## Problem
Detect wake words ("Alexa", "Echo", "Computer", etc.) accurately on-device under tight compute/memory budgets and in noisy conditions, while keeping both false accepts and false rejects low — including when the device itself is emitting sound.

## Approach / System design
A two-stage pipeline: a lightweight on-device detector flags candidate wake words, then a more powerful cloud model verifies them. The on-device model trades compute for a small memory footprint; the cloud model uses more resources for higher accuracy.

## Key decisions
- Metadata-aware on-device model: device type and audio playback state are embedded as vectors and used to modulate convolutional layer normalization, helping the model generalize when the device plays music or speech.
- Cloud verification uses a convolutional-recurrent-attention (CRA) architecture: recurrent layers capture temporal structure (robust to misaligned wake-word timing) and attention re-weights outputs toward verification-critical features.

## Stack
CNNs with multiple filter channels, recurrent layers, attention, log filter-bank energy (LFBE) acoustic features, and ~195-frame windows for the cloud model.

## Results
Metadata-aware model: 14.6% better false-reject rate vs. a baseline CNN. CRA cloud model: 55% false-accept reduction on aligned data (CNN-only 53%) and 60% on misaligned data (CNN-only 31%), versus a DNN-HMM baseline.

## Takeaways
Device context materially changes the acoustic signal, so feeding metadata in helps; recurrent temporal modeling beats spatial filtering when alignment is imperfect; the on-device/cloud split balances compute limits against accuracy.
