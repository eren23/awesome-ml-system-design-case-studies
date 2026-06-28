---
id: cs1360
title: "Hey Siri: An On-device DNN-powered Voice Trigger for Apple's Personal Assistant"
company: Apple
primary_category: audio
sub_category: audio-classification
year: 2017
source_url: https://machinelearning.apple.com/research/hey-siri
tags: [wake-word, voice-trigger, on-device, dnn, keyword-spotting]
---

# Hey Siri: An On-device DNN-powered Voice Trigger for Apple's Personal Assistant
**Apple** · 2017 · [source](https://machinelearning.apple.com/research/hey-siri)

## Problem
Continuously detect "Hey Siri" on-device for hands-free activation while minimizing false positives, false rejects, latency, and battery drain.

## Approach / System design
A two-pass detection design: a small detector runs constantly on the low-power Always-On Processor (AOP); when it fires, it wakes the main processor to run a larger, more accurate second detector. A personalization layer compares utterances against enrolled samples for speaker verification.

## Key decisions
- Two-pass detection to limit main-processor usage and battery drain.
- Adaptive thresholds: a normal threshold plus a lower "second-chance" threshold improves usability without inflating false alarms.
- Speaker enrollment from five "Hey Siri" phrases captured during setup, to reject imposters.
- Temporal integration via dynamic programming to accumulate acoustic scores across frames.

## Stack
DNNs with 5 hidden layers (32/128/192 units depending on device), Mel-filterbank features, HMM-style temporal modeling, ~20 phonetic classes per language variant. Trained with Theano, TensorFlow, and Kaldi.

## Results
Targets a false-accept rate of about one per week; FRR/FAR trade-offs measured on large test sets, with weekly production sampling validating imposter-accept and false-alarm rates on real devices.

## Takeaways
On-device voice triggers need careful memory/power/latency optimization; multi-stage pipelines balance accuracy against compute; offline metrics must be validated against production data; phonetic modeling has to be language-specific.
