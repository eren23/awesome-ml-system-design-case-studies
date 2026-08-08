---
id: cs1805
title: Deepgram — Flux: Fusing Transcription and Conversational State into One Real-Time Model
company: Deepgram
primary_category: audio
sub_category: asr
year: 2025
source_url: https://deepgram.com/learn/fluxing-conversational-state-and-speech-to-text
tags: [asr, conversational-ai, turn-detection, real-time, voice-agents]
---

# Deepgram — Flux: Fusing Transcription and Conversational State into One Real-Time Model
**Deepgram** · 2025 · [source](https://deepgram.com/learn/fluxing-conversational-state-and-speech-to-text)

## Problem
Traditional voice agent pipelines chain separate models for speech-to-text and turn/endpointing detection, which introduces latency between the end of a speaker's utterance and the system's response. The sequential nature of these pipelines means each component operates without awareness of the other's signals, resulting in missed context and slower end-to-end response times.

## Approach / System design
Deepgram's Flux model unifies transcription and conversational state modeling — including turn detection and endpointing — into a single neural network that processes audio in real time. By sharing representations between the transcription and state-detection tasks, the model achieves bidirectional information flow: transcription quality informs turn detection and vice versa, rather than treating them as independent sequential steps.

## Key decisions
Combining both tasks in one model eliminates the pipeline handoff latency that accumulates when a separate endpointing model must wait for a transcription model to produce output before deciding whether a turn has ended. Bidirectional information sharing between tasks also reduces the error cases where a standalone endpointer misclassifies mid-utterance pauses as turn boundaries.

## Stack
Single real-time neural model (Flux) handling joint ASR and conversational state, streaming audio inference infrastructure.

## Results
Not covered in the source.

## Takeaways
Fusing transcription and turn detection into one model removes the latency tax of a multi-model pipeline, which is especially important for voice agents where response delay degrades the conversational experience. Shared representations between jointly trained tasks can improve accuracy on both relative to independently trained models, since the tasks have complementary signal. For voice agents at scale, reducing inference latency at the STT layer has compounding benefits across the entire response pipeline.
