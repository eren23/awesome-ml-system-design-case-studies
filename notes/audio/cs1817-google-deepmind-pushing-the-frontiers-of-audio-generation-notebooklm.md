---
id: cs1817
title: "Google DeepMind — Pushing the Frontiers of Audio Generation (NotebookLM, Illuminate)"
company: Google DeepMind
primary_category: audio
sub_category: speaker-id
year: "2024"
source_url: https://deepmind.google/discover/blog/pushing-the-frontiers-of-audio-generation/
tags: [speech-generation, neural-codec, transformer, notebooklm, auto-dubbing]
---

# Google DeepMind — Pushing the Frontiers of Audio Generation (NotebookLM, Illuminate)
**Google DeepMind** · 2024 · [source](https://deepmind.google/discover/blog/pushing-the-frontiers-of-audio-generation/)

## Problem
Serving high-quality multi-speaker speech synthesis across diverse products — NotebookLM Audio Overviews, Illuminate, Gemini Live, and YouTube auto-dubbing — required a single scalable speech stack capable of handling different speakers, speaking styles, and languages with very low latency on shared infrastructure.

## Approach / System design
The system combines a compact 600 bits-per-second neural audio codec with a Transformer that generates hierarchical tokens representing the codec's output. The codec's high compression ratio keeps the token sequence short, allowing the Transformer to generate two minutes of dialogue in a single forward pass on one TPU without chunking or streaming workarounds.

## Key decisions
Operating at 600 bps is unusually aggressive compression, but it directly determines how long the token sequence is and therefore how fast generation can be; this trade-off between fidelity and sequence length was a deliberate design choice. Sharing the same codec-plus-Transformer stack across NotebookLM, Illuminate, Gemini Live, and YouTube auto-dubbing reduced infrastructure fragmentation and allowed research improvements to propagate across all four products simultaneously.

## Stack
Custom 600 bps neural audio codec, Transformer, Google TPU serving infrastructure.

## Results
The system renders two minutes of multi-speaker dialogue in under three seconds on a single TPU. No additional throughput or quality benchmark figures are covered in the source.

## Takeaways
Extremely compact neural codecs substantially reduce the sequence length that generative models must handle, enabling fast whole-dialogue generation rather than incremental streaming. A unified speech generation stack shared across products lowers maintenance overhead and allows a single research improvement to benefit multiple user-facing applications at once.
