---
id: cs2085
title: Cold-Starting Podcast Ads and Promotions with Multi-Task Learning on Spotify
company: Spotify
primary_category: ads
sub_category: targeting
year: 2026
source_url: https://arxiv.org/abs/2601.02306
tags: [cold-start, multi-task-learning, podcast-ads, transfer-learning, promotions, CTR-prediction]
---

# Cold-Starting Podcast Ads and Promotions with Multi-Task Learning on Spotify
**Spotify** · 2026 · [source](https://arxiv.org/abs/2601.02306)

## Problem
Spotify needed better targeting for podcast ads and in-app promotions, but new advertising objectives arrive with little or no historical interaction data — a cold-start problem. Historically, each targeting objective lived in its own siloed pipeline, multiplying maintenance cost and preventing knowledge sharing across tasks.

## Approach / System design
A single unified multi-objective model trained with multi-task learning over large-scale ad and content interaction data. The model shares representations across user, content, context, and creative features, and jointly optimizes multiple podcast outcomes (streams, clicks, follows). New targeting tasks — including in-app promotions — are cold-started by fine-tuning the joint model, transferring what it learned from data-rich tasks.

## Key decisions
- Replace siloed per-objective targeting pipelines with one unified model serving both ads and promotions.
- Use transfer learning from the shared model as the cold-start mechanism for new objectives rather than building bespoke cold-start heuristics.
- Jointly optimize multiple engagement outcomes (streams, clicks, follows) instead of single-metric models.

## Stack
Multi-task neural model over user/content/context/creative features with fine-tuning for new tasks. Published at WSDM 2026. Specific architectures and serving details are not covered in the source.

## Results
Online A/B tests showed up to a 22% reduction in effective cost-per-stream (eCPS) — with the largest gains for less-streamed podcasts — and an 18–24% increase in podcast stream rates, plus improved cold-start performance and coverage validated offline and online.

## Takeaways
Consolidating siloed targeting systems into one multi-task model paid off three ways at once: better cold-start via transfer, better coverage, and lower maintenance burden — with the biggest wins accruing to long-tail (less-streamed) content.
