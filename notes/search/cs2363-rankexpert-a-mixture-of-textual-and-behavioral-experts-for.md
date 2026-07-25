---
id: cs2363
title: "RankExpert: A Mixture of Textual-and-Behavioral Experts for Multi-Objective Learning-to-Rank in Web Search"
company: Baidu
primary_category: search
sub_category: learning-to-rank
year: 2025
source_url: https://dl.acm.org/doi/10.1145/3711896.3737258
tags: [mixture-of-experts, learning-to-rank, web-search, multi-objective-ranking, behavioral-signals, textual-features]
---

# RankExpert: A Mixture of Textual-and-Behavioral Experts for Multi-Objective Learning-to-Rank in Web Search
**Baidu** · 2025 · [source](https://dl.acm.org/doi/10.1145/3711896.3737258)

## Problem
Production web-search ranking must satisfy several objectives at once — relevance, quality, authority, and recency — while also learning from click feedback that is contaminated by position bias. A single monolithic ranker struggles to optimize these competing objectives and signal types (textual query-document features vs. behavioral feedback) jointly.

## Approach / System design
RankExpert (KDD 2025) is a mixture-of-experts learning-to-rank model that separates textual and behavioral expertise. A lightweight pretrained language model, trained with hierarchical distillation, provides efficient query-document representations. Dedicated experts disentangle and optimize the different ranking objectives (relevance, quality, authority, recency), and a click expert within a dual-tower design mitigates position bias in user feedback. An adaptive weight fusion layer dynamically combines the specialized experts' outputs so the final ranking prediction adapts to diverse user intents.

## Key decisions
- Split ranking objectives across specialized experts instead of blending all signals in one tower.
- Distill a heavy PLM into a lightweight one (hierarchical distillation) to keep textual understanding affordable at web-search serving scale.
- Add a dedicated click expert in a dual-tower arrangement to debias behavioral signals rather than consuming raw clicks.
- Fuse expert outputs with an adaptive, query-dependent weighting layer rather than fixed objective weights.

## Stack
Not covered in the source beyond the model components (lightweight PLM, MoE experts, dual-tower click expert, adaptive fusion layer).

## Results
Offline evaluations on two large-scale real-world datasets showed significant gains over strong competitor models on key performance indicators. Deployed in Baidu Search, online evaluation on real web traffic showed substantial improvements in user satisfaction metrics over the legacy production system.

## Takeaways
Treating multi-objective ranking as a mixture-of-experts problem — with textual and behavioral signals handled by different experts and fused adaptively per query — outperforms monolithic rankers, and explicit position-bias handling (the click expert) is what makes behavioral feedback safe to learn from in production.
