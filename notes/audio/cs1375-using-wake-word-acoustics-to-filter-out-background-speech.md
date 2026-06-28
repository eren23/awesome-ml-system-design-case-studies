---
id: cs1375
title: Using wake word acoustics to filter out background speech improves speech recognition by 15%
company: Amazon (Alexa)
primary_category: audio
sub_category: asr
year: 2019
source_url: https://www.amazon.science/blog/using-wake-word-acoustics-to-filter-out-background-speech-improves-speech-recognition-by-15-percent
tags: [asr, wake-word, background-speech, attention, seq2seq, alexa]
---

# Using wake word acoustics to filter out background speech improves speech recognition by 15%
**Amazon (Alexa)** · 2019 · [source](https://www.amazon.science/blog/using-wake-word-acoustics-to-filter-out-background-speech-improves-speech-recognition-by-15-percent)

## Problem
In multi-speaker rooms, background conversation degrades Alexa's ASR. The system needs to keep speech that was actually directed at the device and suppress everything else.

## Approach / System design
Take an acoustic snapshot of the spoken wake word and compare following speech against it. Speech matching the wake word's acoustic profile is treated as intended for Alexa; non-matching audio is treated as background to suppress. The filtering is integrated directly into a sequence-to-sequence ASR model rather than done as a separate preprocessing step.

## Key decisions
Two variants were compared. The attention-based variant feeds raw wake-word frames into the attention mechanism so the model learns the relevant acoustics itself. The masking-based variant explicitly compares wake-word acoustics to later speech and masks non-matching encoder outputs before attention. Attention slightly won (15% vs. 13% error reduction), likely because it also leverages decoder-state information.

## Stack
Seq2seq encoder-decoder with attention; neural nets over millisecond-scale audio frames; encoder produces fixed-length summary vectors, decoder emits phonetic output.

## Results
The attention approach reduced speech recognition errors by 15% versus the baseline ASR; the masking variant achieved 13%.

## Takeaways
Folding acoustic filtering into the end-to-end ASR beats isolated preprocessing, and an implicit attention mechanism can outperform an explicitly supervised mask when decoder context is useful.
