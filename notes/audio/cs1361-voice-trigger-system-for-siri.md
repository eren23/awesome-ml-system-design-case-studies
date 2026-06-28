---
id: cs1361
title: Voice Trigger System for Siri
company: Apple
primary_category: audio
sub_category: speaker-id
year: 2023
source_url: https://machinelearning.apple.com/research/voice-trigger
tags: [wake-word, voice-trigger, on-device, false-accept, system-design]
---

# Voice Trigger System for Siri
**Apple** · 2023 · [source](https://machinelearning.apple.com/research/voice-trigger)

## Problem
Build a privacy-preserving, low-power, on-device voice trigger that distinguishes the device owner from other speakers, rejects false triggers from noise and phonetically similar phrases, and supports both "Hey Siri" and "Siri" across many locales and device types.

## Approach / System design
A multi-stage cascade: (1) a streaming keyword detector on the Always-On Processor for low-power spotting, (2) a high-precision re-scoring checker on the Application Processor, (3) speaker identification for owner verification, and (4) false-trigger mitigation combining several complementary systems (acoustic, ASR-lattice, and text-semantic signals).

## Key decisions
- Streaming ring-buffer processing for latency.
- End-to-end training of the DNN-HMM detector to align the loss with actual detection metrics.
- 4-bit weight quantization for resource-constrained devices.
- Conformer encoder for a better accuracy/latency trade-off.
- Multiple independent false-trigger-mitigation (FTM) systems leveraging different signal aspects.
- A single multilingual speaker-embedding extractor for better generalization in data-sparse locales.

## Stack
DNN-HMM keyword spotting (21 phoneme states + silence/background), Conformer encoder with CTC plus discriminative loss, LSTM speaker-embedding extractors, latticeRNN for graph-based FTM, a streaming transformer for acoustic FTM, a BERT-based out-of-domain language detector for text FTM, plus differentiable k-means and range regularization for compression.

## Results
The article centers on architecture; it does not report explicit quantitative precision/recall benchmarks.

## Takeaways
Cascaded multi-stage systems balance accuracy, latency, and power; aligning loss with detection metrics helps; fusing acoustic, ASR, and text signals robustly cuts false positives; cross-lingual training strengthens speaker recognition where data is scarce.
