---
id: cs2266
title: Filter-And-Refine: Multimodal LLM Cascade for Industrial Video Content Moderation
company: TikTok
primary_category: moderation
sub_category: policy-enforcement
year: 2025
source_url: https://arxiv.org/abs/2507.17204
tags: [mllm, video-moderation, cascade, two-stage, multimodal, industrial-scale]
---

# Filter-And-Refine: Multimodal LLM Cascade for Industrial Video Content Moderation
**TikTok** · 2025 · [source](https://arxiv.org/abs/2507.17204)

## Problem
Industrial-scale video moderation with traditional classifiers fails on implicitly harmful content and contextually ambiguous cases. Multimodal LLMs handle this nuance better, but two barriers block deployment: running an MLLM on every video is computationally prohibitive, and generative MLLMs are not natively suited to discriminative classification.

## Approach / System design
A two-stage filter-and-refine cascade. First, the generative MLLM is converted into a multimodal classifier via fine-tuning with a small amount of discriminative training data. Second, a lightweight router model screens all incoming videos and forwards only uncertain cases to the MLLM for detailed re-ranking, so the expensive model sees a small slice of traffic while the cheap model handles the clear-cut majority.

## Key decisions
- Cascade (router + MLLM re-ranker) instead of full-scale MLLM deployment, cutting compute to a fraction of direct deployment.
- Adapt a generative MLLM to discriminative moderation with minimal labeled data (~2% of typical fine-tuning data volume).
- Route on uncertainty: the MLLM only refines cases the lightweight model can't confidently decide.

## Stack
Lightweight router/filter classifier plus a fine-tuned multimodal LLM re-ranker (specific model names not disclosed in the abstract). Published at ACL 2025 Industry Track.

## Results
- 66.50% F1 improvement over traditional classifiers.
- Achieved using only 2% of the typical fine-tuning data.
- Automatic moderation volume increased by 41% in the industrial deployment.
- Cascade deployment costs 1.5% of the compute of full-scale MLLM deployment.

## Takeaways
Cascades make MLLMs economically viable for industrial moderation: reserve the expensive model for ambiguous content and let a cheap filter absorb the bulk. Generative MLLMs can be turned into strong discriminative classifiers with surprisingly little labeled data, and the accuracy gains translate directly into more content moderated automatically.
