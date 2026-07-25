---
id: cs2140
title: UNIVID: Unified Vision-Language Model for Video Moderation
company: ByteDance
primary_category: moderation
sub_category: policy-enforcement
year: 2026
source_url: https://arxiv.org/abs/2606.05748
tags: [vlm, unified-model, video-moderation, industrial-scale, production, caption-generation]
---

# UNIVID: Unified Vision-Language Model for Video Moderation
**ByteDance** · 2026 · [source](https://arxiv.org/abs/2606.05748)

## Problem
Video moderation at industrial scale demands both multi-modal reasoning and transparency about why content was actioned. ByteDance's legacy setup relied on a fragmented fleet of over 1,000 policy-specific classifiers — opaque, expensive to maintain, and hard to audit when enforcement decisions needed justification.

## Approach / System design
UNIVID is a single unified vision-language model that replaces the classifier fleet. Instead of emitting binary labels directly, it generates policy-aware captions — natural-language descriptions of what in the video relates to which policy — which act as an interpretable intermediate representation. Downstream enforcement decisions and multiple workflows then reuse this shared textual output, so one backbone serves many policy tasks.

## Key decisions
- Caption generation as a proxy for classification, so every decision comes with a human-verifiable explanation.
- Consolidate 1,000+ specialized policy models into one shared VLM backbone.
- Build custom training data mixing expert-refined labels with synthetic examples aligned to safety guidelines, specifically to avoid the safety-guardrail refusal behavior that off-the-shelf VLMs exhibit on moderation content.

## Stack
Fine-tuned vision-language model; training corpus combining human-annotated and synthetic moderation data. Specific base model and serving details are not covered in the source.

## Results
- 42.7% reduction in violation leakage (missed violations).
- 37.0% reduction in overkill rate (false positives).
- Retired 1,000+ individual policy models, recovering significant compute.

## Takeaways
- An interpretable intermediate representation (captions) can improve both accuracy and auditability at the same time.
- Model consolidation is a maintenance and cost win as much as a quality win: one backbone beats a thousand narrow classifiers.
- Off-the-shelf VLM safety refusals are a real obstacle for moderation use cases; purpose-built training data is needed to work around them.
