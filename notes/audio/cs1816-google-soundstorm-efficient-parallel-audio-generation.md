---
id: cs1816
title: "Google — SoundStorm: Efficient Parallel Audio Generation"
company: Google
primary_category: audio
sub_category: audio-classification
year: "2023"
source_url: https://research.google/blog/soundstorm-efficient-parallel-audio-generation/
tags: [audio-generation, non-autoregressive, conformer, soundstream, parallel-decoding]
---

# Google — SoundStorm: Efficient Parallel Audio Generation
**Google** · 2023 · [source](https://research.google/blog/soundstorm-efficient-parallel-audio-generation/)

## Problem
Autoregressive audio generation models such as AudioLM produce high-quality speech and audio but are prohibitively slow for practical deployment because they must generate tokens one at a time across multiple residual vector quantization codebook levels. Reducing generation time while preserving perceived quality was the core challenge.

## Approach / System design
SoundStorm is a bidirectional Conformer that operates on SoundStream's residual vector quantization (RVQ) tokens and generates them level by level rather than token by token. Within each codebook level, a confidence-based parallel decoding strategy allows multiple tokens to be committed simultaneously, collapsing the sequential bottleneck that autoregressive models face.

## Key decisions
Using a non-autoregressive, iterative refinement approach rather than a fully autoregressive decoder was the central design bet, trading some architectural simplicity for a large speedup. The confidence-based masking mechanism determines which tokens are certain enough to commit at each decoding step, allowing the model to parallelise aggressively without degrading quality below the AudioLM threshold.

## Stack
Bidirectional Conformer, SoundStream neural audio codec, RVQ token representation.

## Results
SoundStorm generates audio at approximately 100 times the speed of comparable autoregressive generation while matching AudioLM quality. No wall-clock latency figures are provided in the source.

## Takeaways
Non-autoregressive parallel decoding at the codec-token level is a viable path to production-speed high-fidelity audio generation. Structuring generation level by level in the RVQ hierarchy preserves the quality benefits of multi-codebook audio codecs while enabling parallelism.
