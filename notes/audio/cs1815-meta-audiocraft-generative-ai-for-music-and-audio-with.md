---
id: cs1815
title: "Meta — AudioCraft: Generative AI for Music and Audio with MusicGen, AudioGen, and EnCodec"
company: Meta
primary_category: audio
sub_category: music
year: "2023"
source_url: https://ai.meta.com/blog/audiocraft-musicgen-audiogen-encodec-generative-ai-audio/
tags: [music-generation, encodec, language-model, token-interleaving, audiogen]
---

# Meta — AudioCraft: Generative AI for Music and Audio with MusicGen, AudioGen, and EnCodec
**Meta** · 2023 · [source](https://ai.meta.com/blog/audiocraft-musicgen-audiogen-encodec-generative-ai-audio/)

## Problem
High-quality open-source generative models for music and environmental sound did not exist in an accessible, unified framework. Researchers and developers had no standard toolkit for text-to-audio generation that covered both music and general sound effects at production-relevant quality.

## Approach / System design
AudioCraft treats audio generation as a sequence modelling problem by first compressing raw waveforms into discrete tokens with the EnCodec neural audio codec, then training an autoregressive language model to generate those tokens conditioned on text descriptions. A token-interleaving pattern across EnCodec's multiple codebook streams allows the LM to model the dependencies between streams without a separate hierarchical model. MusicGen handles music generation and AudioGen handles environmental sound effects, both built on the same underlying framework.

## Key decisions
Using EnCodec's multi-codebook representation as the discrete vocabulary was critical — it preserves enough audio fidelity for music generation while keeping vocabulary size tractable for a language model. The token-interleaving pattern was chosen to allow a single flat-sequence LM to capture inter-codebook dependencies without requiring a separate cascade of models. Training on licensed music and publicly available sound data was an explicit choice to respect intellectual property.

## Stack
EnCodec neural audio codec, autoregressive Transformer language model, MusicGen, AudioGen.

## Results
Not covered in the source.

## Takeaways
Neural audio codecs are the enabling technology that makes treating audio generation as language modelling practical: the codec's compression determines sequence length, and the codebook structure determines the vocabulary the LM must learn. Releasing AudioCraft as an open-source framework established a shared foundation for the audio generation research community.
