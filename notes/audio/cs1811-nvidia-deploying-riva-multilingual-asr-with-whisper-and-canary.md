---
id: cs1811
title: "NVIDIA — Deploying Riva Multilingual ASR with Whisper and Canary Architectures"
company: NVIDIA
primary_category: audio
sub_category: asr
year: "2025"
source_url: https://developer.nvidia.com/blog/deploying-nvidia-riva-multilingual-asr-with-whisper-and-canary-architectures-while-selectively-deactivating-nmt/
tags: [asr, riva, whisper, canary, deployment, ssml]
---

# NVIDIA — Deploying Riva Multilingual ASR with Whisper and Canary Architectures
**NVIDIA** · 2025 · [source](https://developer.nvidia.com/blog/deploying-nvidia-riva-multilingual-asr-with-whisper-and-canary-architectures-while-selectively-deactivating-nmt/)

## Problem
Production multilingual ASR deployments that include neural machine translation (NMT) will blindly translate proper nouns, brand names, and technical terms that should remain in their original form. Customers needed a mechanism to exempt specific vocabulary from translation without retraining the underlying models.

## Approach / System design
NVIDIA Riva is configured to serve Whisper, Distil-Whisper, and Canary models for offline transcription and translation. To give operators fine-grained translation control, Riva supports SSML `<dnt>` (do-not-translate) tags that can be embedded in input or output text, as well as do-not-translate dictionaries that map specific terms to their desired pass-through form. When the NMT stage encounters a tagged term or a dictionary entry, it skips translation for that span.

## Key decisions
Reusing established model architectures (Whisper and Canary) rather than training new ones kept the deployment straightforward and the quality baseline well-understood. Using SSML annotation as the control surface for selective NMT deactivation leverages an existing markup standard that integration teams are familiar with, lowering the adoption barrier.

## Stack
NVIDIA Riva serving framework, Whisper, Distil-Whisper, Canary, SSML markup, do-not-translate dictionaries.

## Results
Not covered in the source.

## Takeaways
Production NMT in ASR pipelines requires vocabulary-level control mechanisms; end-to-end neural translation without guardrails will consistently mistranslate domain-specific terminology. SSML is a practical standard for expressing these constraints because it is already supported in many speech toolchains.
