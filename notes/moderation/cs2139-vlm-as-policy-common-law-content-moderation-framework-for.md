---
id: cs2139
title: VLM as Policy: Common-Law Content Moderation Framework for Short Video Platform (KuaiMod)
company: Kuaishou
primary_category: moderation
sub_category: policy-enforcement
year: 2025
source_url: https://arxiv.org/abs/2504.14904
tags: [vlm, chain-of-thought, video-moderation, production, short-video, curriculum-training]
---

# VLM as Policy: Common-Law Content Moderation Framework for Short Video Platform (KuaiMod)
**Kuaishou** · 2025 · [source](https://arxiv.org/abs/2504.14904)

## Problem
Short-video moderation has to protect users (especially minors) at massive scale, but each existing option is flawed: manual review is costly and biased, automated classifiers lack nuance, and static industrial rulebooks cannot keep pace with fast-evolving harmful trends on the platform.

## Approach / System design
KuaiMod treats moderation like common law rather than fixed statute — policy evolves case by case. Three components:
1. **Benchmark / training data construction:** the first short-video-platform moderation benchmark built from authentic user and reviewer feedback.
2. **Offline adaptation:** a vision-language model with chain-of-thought reasoning learns to model video toxicity from sparse feedback signals.
3. **Online deployment and refinement:** the deployed model's policy is dynamically updated, enabling rapid iteration while keeping accuracy high.

## Key decisions
- Chose a VLM with CoT reasoning over traditional classification, to capture the nuance classifiers miss.
- Adopted the "common-law" framing: case-by-case policy refinement instead of a fixed rule set, so the system adapts to emerging content trends.
- Grounded continuous learning in real user feedback signals rather than only curated labels.

## Stack
Vision-language model with chain-of-thought reasoning; benchmark dataset with authentic user/reviewer annotations. Specific base model and serving details are not covered in the source.

## Results
- 20% reduction in user reporting/complaint rates after deployment.
- Increased daily active users and app usage time across multiple Kuaishou scenarios.
- Outperformed baseline methods on the constructed benchmark, serving a platform with hundreds of millions of users.

## Takeaways
- Reasoning-capable VLMs let moderation systems explain and adapt, not just classify.
- Treating policy as a living, feedback-driven artifact (common law) fits fast-moving UGC platforms better than static rules.
- Better moderation showed up in growth metrics (DAU, usage time), not just safety metrics.
