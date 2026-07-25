---
id: cs2100
title: "Identify Speakers in Meetings, Calls, and Voice Apps in Real-Time with NVIDIA Streaming Sortformer"
company: NVIDIA
primary_category: audio
sub_category: speaker-id
year: 2025
source_url: https://developer.nvidia.com/blog/identify-speakers-in-meetings-calls-and-voice-apps-in-real-time-with-nvidia-streaming-sortformer/
tags: [speaker-diarization, streaming, real-time, NeMo, Arrival-Order-Speaker-Cache]
---

# Identify Speakers in Meetings, Calls, and Voice Apps in Real-Time with NVIDIA Streaming Sortformer
**NVIDIA** · 2025 · [source](https://developer.nvidia.com/blog/identify-speakers-in-meetings-calls-and-voice-apps-in-real-time-with-nvidia-streaming-sortformer/)

## Problem
Answering "who is speaking, and when?" live — for meetings, contact centers, and voicebots — is hard: classic diarization runs offline in batch over full recordings, and streaming approaches struggle to keep speaker labels consistent over time without specialized equipment.

## Approach / System design
Streaming Sortformer is a real-time speaker diarization model that processes audio in small overlapping chunks with a FIFO queue rather than analyzing whole recordings. Its core innovation is the Arrival-Order Speaker Cache (AOSC): a memory buffer of embeddings for previously detected speakers, against which each new chunk is compared, so speakers keep consistent labels (spk_0, spk_1, ...) in order of first appearance throughout the stream. The model itself stacks a convolutional pre-encode module (compressing raw audio), Conformer blocks, and transformer blocks for conversational context, trained with a hybrid objective combining sort-loss and permutation-invariant loss. Output is frame-level speaker activity with precise timestamps.

## Key decisions
- Sort speakers by arrival order instead of solving a global permutation problem — this is what makes low-latency streaming diarization with stable labels tractable.
- Chunk-wise processing with a bounded speaker cache to cap memory/latency for long streams.
- Ship through the existing NeMo/Riva ecosystem and on Hugging Face rather than as a standalone tool, so it slots into ASR/TTS/translation pipelines.

## Stack
NVIDIA NeMo and NVIDIA Riva for production deployment; convolutional pre-encoder + Conformer + transformer architecture; model weights published on Hugging Face.

## Results
- Tracks up to four simultaneous speakers in real time with frame-level precision (performance degrades beyond four).
- Outperforms comparable streaming diarization systems (EEND-GLA, LS-EEND) on Diarization Error Rate on evaluated benchmarks.
- Optimized for English but performed well on Mandarin and CALLHOME non-English test data; fine-tuning recommended for domain- or language-specific gains.

## Takeaways
- The arrival-order cache reframes streaming diarization: keep an ordered memory of who has spoken rather than re-clustering, enabling consistent live labels.
- A hard cap (four speakers) is an explicit, documented design trade-off for real-time performance.
- Distributing production speech models through an established ecosystem (NeMo/Riva/HF) shortens the path from research to deployed pipelines.
