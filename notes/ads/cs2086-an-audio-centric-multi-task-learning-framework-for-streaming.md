---
id: cs2086
title: An Audio-centric Multi-task Learning Framework for Streaming Ads Targeting on Spotify
company: Spotify
primary_category: ads
sub_category: ctr-prediction
year: 2025
source_url: https://arxiv.org/abs/2506.18735
tags: [audio-ads, multi-task-learning, mixture-of-experts, CTR-prediction, multi-modal, cross-modal]
---

# An Audio-centric Multi-task Learning Framework for Streaming Ads Targeting on Spotify
**Spotify** · 2025 · [source](https://arxiv.org/abs/2506.18735)

## Problem
Spotify serves ads across an audio-first ecosystem (music, podcasts, audiobooks, plus video and display formats). CTR models built for single-format experiences optimize poorly across these modalities — improving video or display performance can come at the expense of audio ads, which are central to the platform.

## Approach / System design
CAMoE (Cross-modal Adaptive Mixture-of-Experts) is a CTR prediction model that treats each ad modality's prediction as related tasks in a mixture-of-experts framework. Three mechanisms carry the design: modality-aware task grouping (tasks organized around ad format so experts specialize sensibly), adaptive loss masking (format-specific optimization so one modality's gradient signal doesn't wash out another's), and deep-cross networks (DCN) to capture feature interactions across modalities. The goal is a Pareto-optimal balance across audio, video, and display rather than maximizing one format.

## Key decisions
- Group tasks by modality inside the MoE rather than training per-format models or one undifferentiated multi-task model.
- Mask losses adaptively per format to prevent cross-modality interference during training.
- Optimize explicitly for balance across formats (Pareto framing) with audio treated as first-class given the platform's audio-centrality.

## Stack
Mixture-of-experts CTR architecture with DCN feature-interaction layers, deployed in Spotify's ads targeting stack. Presented at KDD 2025. Specific serving infrastructure is not covered in the source.

## Results
In production at scale: +14.5% CTR for audio ads, +1.3% CTR for video ads, and a 4.8% reduction in expected cost-per-click for audio slots, with significant AUC-PR improvements over baselines offline.

## Takeaways
For multi-format ad platforms, modality is the right axis for task grouping in multi-task CTR models; adaptive loss masking plus expert specialization lets a single model lift the core format (audio) substantially without degrading the others.
