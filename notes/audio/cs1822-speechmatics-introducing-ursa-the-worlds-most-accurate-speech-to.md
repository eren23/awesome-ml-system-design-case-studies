---
id: cs1822
title: "Speechmatics — Introducing Ursa: The World's Most Accurate Speech-to-Text"
company: Speechmatics
primary_category: audio
sub_category: asr
year: "2023"
source_url: https://www.speechmatics.com/company/articles-and-news/introducing-ursa-the-worlds-most-accurate-speech-to-text
tags: [asr, self-supervised-learning, model-scaling, multilingual, gpu-inference]
---

# Speechmatics — Introducing Ursa: The World's Most Accurate Speech-to-Text
**Speechmatics** · 2023 · [source](https://www.speechmatics.com/company/articles-and-news/introducing-ursa-the-worlds-most-accurate-speech-to-text)

## Problem
Achieving high accuracy across 50 languages with supervised learning alone is impractical because labelled speech data is scarce for most of those languages. Speechmatics needed a way to leverage the abundant unlabelled audio available across many languages while still producing a model suitable for GPU-accelerated production inference.

## Approach / System design
Ursa is a three-stage pipeline. First, a 2-billion-parameter Transformer is pretrained using self-supervised learning on over one million hours of unlabelled audio spanning 50 languages, building broad acoustic representations without any transcriptions. Second, a separate acoustic phoneme model converts those representations into phoneme sequences. Third, a language model scaled 30 times larger than prior versions post-processes the phoneme output into final transcriptions, contributing heavily to the accuracy gains.

## Key decisions
Self-supervised pretraining at 2 billion parameters and one million hours of unlabelled audio was a deliberate investment to reduce dependence on scarce labelled data while building robust multilingual acoustic features. Scaling the language model by 30x relative to prior systems was a distinct investment from the acoustic side, reflecting the view that language model quality is an underexploited lever in ASR accuracy.

## Stack
2B-parameter self-supervised Transformer, acoustic phoneme model, 30x-scaled language model, GPU-accelerated inference.

## Results
Ursa covers 50 languages and was trained on over 1 million hours of unlabelled audio. Speechmatics claimed it as the world's most accurate ASR at launch; specific WER benchmarks by language are not covered in the source.

## Takeaways
Combining massive self-supervised acoustic pretraining with an independently scaled language model addresses two complementary bottlenecks in multilingual ASR: data scarcity and language model capacity. GPU-accelerated serving is a prerequisite for making a 2B-parameter model commercially viable, reinforcing that hardware efficiency planning must happen alongside model architecture decisions.
