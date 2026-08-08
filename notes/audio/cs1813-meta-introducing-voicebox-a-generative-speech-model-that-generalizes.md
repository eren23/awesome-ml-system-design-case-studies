---
id: cs1813
title: "Meta — Introducing Voicebox: A Generative Speech Model that Generalizes Across Tasks"
company: Meta
primary_category: audio
sub_category: tts
year: "2023"
source_url: https://ai.meta.com/blog/voicebox-generative-ai-model-speech/
tags: [tts, flow-matching, non-autoregressive, speech-generation, audio-editing]
---

# Meta — Introducing Voicebox: A Generative Speech Model that Generalizes Across Tasks
**Meta** · 2023 · [source](https://ai.meta.com/blog/voicebox-generative-ai-model-speech/)

## Problem
Conventional TTS models are trained for a specific task — synthesis, voice conversion, or noise removal — and perform poorly when asked to do anything outside their training objective. Building a separate model for each speech task is expensive, and none of the resulting systems can generalise to novel tasks at inference time without re-training.

## Approach / System design
Voicebox is a non-autoregressive flow-matching model that frames speech synthesis as masked audio infilling: it is trained to regenerate masked spans of speech from the surrounding unmasked audio and corresponding text. Because the model learns to fill in arbitrary gaps given context, it can handle synthesis, editing, noise removal, and cross-lingual style transfer using the same weights by simply masking different portions of the input at inference time.

## Key decisions
Flow-matching was selected as the generative framework because it is non-autoregressive and supports high-quality continuous-valued sample generation without the discretisation required by token-based approaches. Formulating training as context-conditioned infilling rather than left-to-right generation was the key insight that unlocks zero-shot generalisation: the model implicitly learns what speech "should" sound like given its surroundings.

## Stack
Flow-matching continuous normalising flow, non-autoregressive architecture; trained on over 50,000 hours of speech across six languages.

## Results
Voicebox was trained on over 50,000 hours of data covering six languages and supports synthesis, editing, noise removal, and style transfer without any task-specific fine-tuning. No specific word error rate or naturalness benchmark figures are covered in the source.

## Takeaways
Framing speech generation as masked in-context infilling converts a task-specific system into a general-purpose one, dramatically expanding what a single model can do at inference time. Flow-matching is well suited to this formulation because it produces high-quality continuous audio samples efficiently in a non-autoregressive fashion.
