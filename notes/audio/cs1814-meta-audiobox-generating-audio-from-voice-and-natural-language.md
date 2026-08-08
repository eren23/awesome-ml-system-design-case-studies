---
id: cs1814
title: "Meta — Audiobox: Generating Audio from Voice and Natural Language Prompts"
company: Meta
primary_category: audio
sub_category: audio-classification
year: "2023"
source_url: https://ai.meta.com/blog/audiobox-generating-audio-voice-natural-language-prompts/
tags: [audio-generation, flow-matching, tts, sound-effects, controllability]
---

# Meta — Audiobox: Generating Audio from Voice and Natural Language Prompts
**Meta** · 2023 · [source](https://ai.meta.com/blog/audiobox-generating-audio-voice-natural-language-prompts/)

## Problem
Prior audio generation systems were siloed: speech synthesis, sound effect generation, and environmental soundscape synthesis were handled by separate models with separate interfaces. There was no unified system that could generate any category of audio under consistent, natural-language-driven control.

## Approach / System design
Audiobox extends Voicebox's flow-matching non-autoregressive framework with a guided generation objective that conditions jointly on voice reference prompts and free-form natural language text descriptions. This shared conditioning mechanism allows a single model to generate speech, sound effects, and soundscapes by varying only the combination of voice and text prompts provided at inference time.

## Key decisions
Building on Voicebox's flow-matching foundation rather than starting from scratch gave Audiobox a strong continuous normalising-flow base that naturally supports interpolation and controlled generation. Combining voice-based style prompting with natural-language description was the key architectural choice that enabled cross-domain controllability without requiring domain-specific model heads.

## Stack
Flow-matching generative model, Voicebox-based architecture, voice and text conditioning.

## Results
Not covered in the source.

## Takeaways
Unifying speech, sound effect, and soundscape generation under one model with a shared controllable prompting interface simplifies the audio production pipeline and enables novel creative combinations. Flow-matching provides a particularly clean framework for conditional audio generation because it allows flexible guidance at inference time.
