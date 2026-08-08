---
id: cs1809
title: "NVIDIA — Pushing the Boundaries of Speech Recognition with NeMo Parakeet ASR Models"
company: NVIDIA
primary_category: audio
sub_category: asr
year: "2024"
source_url: https://developer.nvidia.com/blog/pushing-the-boundaries-of-speech-recognition-with-nemo-parakeet-asr-models/
tags: [asr, fast-conformer, rnnt, ctc, long-form-audio]
---

# NVIDIA — Pushing the Boundaries of Speech Recognition with NeMo Parakeet ASR Models
**NVIDIA** · 2024 · [source](https://developer.nvidia.com/blog/pushing-the-boundaries-of-speech-recognition-with-nemo-parakeet-asr-models/)

## Problem
Transcribing long recordings — meetings, lectures, podcasts — pushes standard ASR models to their limits because attention complexity grows quadratically with sequence length and most models assume short utterances. Simultaneously, deployment scenarios range from latency-sensitive streaming to throughput-focused offline batch jobs, requiring models at different size and accuracy operating points.

## Approach / System design
Parakeet models are built on the Fast Conformer encoder, which uses depthwise-separable convolutions with an 8x temporal downsampling stride and limits self-attention to a local context window. The reduced sequence length from aggressive downsampling allows the model to process audio as long as 11 hours without truncation. Two model sizes — 0.6 billion and 1.1 billion parameters — are offered, paired with either RNN-T or CTC decoder heads to cover streaming and offline use cases respectively.

## Key decisions
The 8x downsampling stride was chosen specifically to bring very long audio into a manageable sequence length for attention; without it, hour-long recordings would be infeasible. Offering two parameter counts rather than a single flagship model acknowledges the real deployment tension between accuracy and compute budget.

## Stack
Fast Conformer encoder, depthwise-separable convolutions, RNN-T decoder, CTC decoder, NVIDIA NeMo framework.

## Results
Parakeet models can transcribe continuous audio up to 11 hours in length. The family is available in 0.6B and 1.1B parameter variants. Specific WER figures are not covered in the source.

## Takeaways
Aggressive temporal downsampling inside the encoder is the key design lever that makes practical long-form ASR possible; without it, attention costs make long recordings infeasible regardless of hardware. Providing multiple model sizes with different decoder heads makes a single architectural family serve both latency-sensitive and throughput-sensitive production scenarios.
