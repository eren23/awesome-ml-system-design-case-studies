---
id: cs1821
title: Amazon — Alexa Unveils New Speech Recognition and Text-to-Speech Technologies
company: Amazon
primary_category: audio
sub_category: asr
year: 2023
source_url: https://www.amazon.science/blog/alexa-unveils-new-speech-recognition-text-to-speech-technologies
tags: [asr, tts, speech-to-speech, gpu-acceleration, llm]
---

# Amazon — Alexa Unveils New Speech Recognition and Text-to-Speech Technologies
**Amazon** · 2023 · [source](https://www.amazon.science/blog/alexa-unveils-new-speech-recognition-text-to-speech-technologies)

## Problem
Make Alexa interactions feel more natural and conversational by improving recognition accuracy, producing more expressive synthesized speech, and reducing the awkwardness of pipelines that pass through intermediate text representations.

## Approach / System design
Three new systems are introduced. A GPU-accelerated ASR model batches audio frames for parallel processing and uses dynamic lookahead (peeking at future frames as context). A large multispeaker/multilingual TTS model is trained on thousands of hours of audio for richer expressivity. An LLM-based end-to-end speech-to-speech model generates output speech directly from input speech using a shared encoding that captures both semantic and acoustic features, adding humanlike prosody, laughter and other paralinguistics.

## Key decisions
- Moved ASR from CPU to GPU so frames can be batched and processed in parallel, which in turn enabled the dynamic-lookahead accuracy gains.
- Added a two-pass end-pointer that combines transcription with acoustic encoding to better detect end-of-turn during natural pauses.
- Jointly fine-tuned the text-to-text LLM and the speech synthesizer so generated text is tailored to synthesis.
- Used a unified input/output encoding in the speech-to-speech model so it can skip the text bottleneck.

## Stack
Multibillion-parameter ASR model with LLM-based rescoring; large TTS (LTTS) trained on thousands of hours of multispeaker, multilingual audio; speech-to-speech LLM built on a pretrained foundation model.

## Results
The article is forward-looking and does not give quantitative benchmarks. It states the ASR model was planned to roll out later that year, with LTTS and speech-to-speech the following year.

## Takeaways
Scaling training data (thousands of hours vs. ~100) buys expressivity; architectural choices compound (GPU batching unlocked lookahead); jointly optimized end-to-end models can beat staged pipelines.
