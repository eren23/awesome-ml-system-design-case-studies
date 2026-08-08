---
id: cs1804
title: "Deepgram — Nova-2: Building the Fastest, Most Accurate Speech-to-Text API"
company: Deepgram
primary_category: audio
sub_category: asr
year: "2023"
source_url: https://deepgram.com/learn/nova-2-speech-to-text-api
tags: [asr, transformer, multi-stage-training, data-curation, inference-latency]
---

# Deepgram — Nova-2: Building the Fastest, Most Accurate Speech-to-Text API
**Deepgram** · 2023 · [source](https://deepgram.com/learn/nova-2-speech-to-text-api)

## Problem
Deepgram needed to push the accuracy ceiling of its production speech-to-text API while keeping latency low enough for real-time applications. The predecessor model, Nova-1, had established a baseline for speed, but further word error rate reductions required rethinking both the training data pipeline and the learning curriculum.

## Approach / System design
Nova-2 is built around a speech-optimized Transformer architecture trained through a two-stage curriculum: an initial broad pre-training phase followed by a targeted fine-tuning stage that focuses the model on harder acoustic conditions. Alongside the architecture, the team invested heavily in data curation to remove noise and improve label quality before any model training began.

## Key decisions
Adopting a two-stage training curriculum was a deliberate choice to separate generic acoustic representation learning from domain-specific refinement, which allowed each stage to be tuned independently. Data curation was treated as a first-class concern rather than an afterthought, with systematic filtering applied upstream of training to ensure the model learned from clean signal.

## Stack
Speech-optimized Transformer architecture; custom multi-stage training pipeline; proprietary data curation tooling.

## Results
Nova-2 reduced word error rate by approximately 18% compared to Nova-1 while maintaining the inference speed that production deployments require. No further latency or throughput figures are covered in the source.

## Takeaways
Combining rigorous data curation with a staged training curriculum produces meaningful accuracy gains without sacrificing the inference speed needed for real-time ASR products. Architecture improvements alone are insufficient if training data quality is left unaddressed.
