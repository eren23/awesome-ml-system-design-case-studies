---
id: cs2186
title: "Ursa 2: Elevating Speech Recognition Across 52 Languages"
company: Speechmatics
primary_category: audio
sub_category: asr
year: 2024
source_url: https://www.speechmatics.com/company/articles-and-news/ursa-2-elevating-speech-recognition-across-52-languages
tags: [ASR, multilingual, hybrid-architecture, code-switching, WER, large-scale-pretraining]
---

# Ursa 2: Elevating Speech Recognition Across 52 Languages
**Speechmatics** · 2024 · [source](https://www.speechmatics.com/company/articles-and-news/ursa-2-elevating-speech-recognition-across-52-languages)

## Problem
ASR accuracy is inconsistent across languages, dialects, and accents, and transcription errors compound in every downstream application built on the transcript — so the foundation model needs reliable accuracy everywhere, not just peak scores on a few major languages.

## Approach / System design
Ursa 2 scales Speechmatics' self-supervised learning recipe: pretraining on vast amounts of unlabeled audio (the post's analogy is a child learning languages by immersion) followed by targeted per-language fine-tuning. Versus Ursa 1, training data grew from 1.3M to 2.8M hours and parameters from 2.07B to 2.88B, with inference moved entirely to GPU and optimized for real-time latency.

## Key decisions
- Scale both pretraining data (2.8M hours) and model size (2.88B parameters) rather than per-language specialization.
- Optimize for consistency across all languages instead of peak accuracy on individual ones.
- Move fully to GPU inference while keeping real-time, sub-second latency.
- Extend coverage to underrepresented languages such as Irish and Maltese.

## Stack
Self-supervised pretraining on unlabeled audio plus supervised fine-tuning; 2.88B-parameter model trained on 2.8M hours; GPU-based real-time inference serving 50+ languages.

## Results
18% average word-error-rate reduction across 50 languages versus Ursa 1; sub-1-second real-time latency; ranked most accurate on 62% of languages and top-three on 92%; standout gains include a 57.3% WER reduction for Vietnamese and improved Arabic dialect handling.

## Takeaways
For speech infrastructure, consistent accuracy beats headline peak accuracy: downstream systems inherit every transcription error, so evenness across languages, dialects, and accents is the product requirement — achieved here mainly by scaling self-supervised pretraining.
