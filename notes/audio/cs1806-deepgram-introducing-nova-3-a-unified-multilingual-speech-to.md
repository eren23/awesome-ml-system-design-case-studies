---
id: cs1806
title: Deepgram — Introducing Nova-3: A Unified Multilingual Speech-to-Text Model with Keyterm Prompting
company: Deepgram
primary_category: audio
sub_category: audio-classification
year: 2025
source_url: https://deepgram.com/learn/introducing-nova-3-speech-to-text-api
tags: [asr, multilingual, representation-learning, in-context-learning, keyterm-prompting]
---

# Deepgram — Introducing Nova-3: A Unified Multilingual Speech-to-Text Model with Keyterm Prompting
**Deepgram** · 2025 · [source](https://deepgram.com/learn/introducing-nova-3-speech-to-text-api)

## Problem
Domain-specific ASR applications — such as medical transcription or legal recording — require accurate recognition of specialized vocabulary and proper nouns that a general-purpose model has rarely encountered. Traditionally, adapting a speech model to a domain requires fine-tuning on domain-specific data, which is expensive and creates a proliferation of specialized model variants to maintain.

## Approach / System design
Nova-3 is a unified multilingual model that learns a shared audio embedding space capable of representing speech across languages. It incorporates a trained contextual mechanism that accepts up to 100 user-provided keyterms at inference time, boosting the likelihood of those terms in the output without any retraining. This Keyterm Prompting feature works analogously to in-context learning — domain adaptation happens at request time rather than at training time.

## Key decisions
Building Keyterm Prompting as a trained inference-time mechanism rather than a simple score-boosting heuristic allows the model to integrate domain context more naturally into beam search and decoding, producing better transcriptions of specialized terms in their surrounding linguistic context. A unified multilingual architecture reduces model proliferation by consolidating language-specific variants into one deployable artifact.

## Stack
Nova-3 unified multilingual ASR model, learned audio embeddings, trained contextual mechanism for Keyterm Prompting, inference-time term injection (up to 100 terms per request).

## Results
Not covered in the source.

## Takeaways
Inference-time domain adaptation via keyterm prompting provides a practical alternative to per-domain fine-tuning, making it feasible for customers to improve ASR accuracy on specialized vocabulary without submitting training data or waiting for model retraining. A unified multilingual model simplifies deployment for customers with multilingual transcription needs. Learned contextual adaptation mechanisms are more robust than post-processing score boosts because they operate within the model's generative process rather than on top of it.
