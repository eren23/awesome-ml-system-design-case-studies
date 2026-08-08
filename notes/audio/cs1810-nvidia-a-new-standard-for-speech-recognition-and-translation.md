---
id: cs1810
title: "NVIDIA — A New Standard for Speech Recognition and Translation with the NeMo Canary Model"
company: NVIDIA
primary_category: audio
sub_category: asr
year: "2024"
source_url: https://developer.nvidia.com/blog/new-standard-for-speech-recognition-and-translation-from-the-nvidia-nemo-canary-model/
tags: [asr, speech-translation, encoder-decoder, fast-conformer, multilingual]
---

# NVIDIA — A New Standard for Speech Recognition and Translation with the NeMo Canary Model
**NVIDIA** · 2024 · [source](https://developer.nvidia.com/blog/new-standard-for-speech-recognition-and-translation-from-the-nvidia-nemo-canary-model/)

## Problem
Deploying separate models for transcription and for speech translation across multiple languages increases infrastructure complexity and maintenance burden. A single encoder-decoder model that handles both tasks across the target language set would simplify deployment while maintaining competitive accuracy.

## Approach / System design
Canary uses a Fast-Conformer encoder paired with an autoregressive Transformer decoder. Language identity and task type are signalled through special prompt tokens prepended to each decoder input, allowing a single model to switch between transcription and translation at inference time. A concatenated tokenizer that spans all target languages gives the decoder a shared vocabulary for English, Spanish, German, and French.

## Key decisions
Selecting Fast-Conformer as the encoder provides efficient long-context acoustic modelling while keeping encoder compute manageable. Task-prompting via special tokens rather than through separate decoder heads was the key design choice that avoided duplicating model parameters for each task and language pair.

## Stack
Fast-Conformer encoder, autoregressive Transformer decoder, concatenated multilingual tokenizer, NVIDIA NeMo framework.

## Results
Canary covers ASR transcription and speech translation across English, Spanish, German, and French. Specific WER or BLEU scores are not covered in the source.

## Takeaways
Task-prompting with special tokens is an effective way to extend an ASR encoder-decoder to translation without separate model training runs, reducing infrastructure complexity without meaningfully sacrificing accuracy. A shared multilingual tokenizer is a prerequisite for this approach to work cleanly across target languages.
