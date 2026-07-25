---
id: cs2347
title: "Sentinel: Roblox's Open-Source Contrastive Learning Library for Detecting Rare Harmful Text in Real-Time"
company: Roblox
primary_category: moderation
sub_category: policy-enforcement
year: 2025
source_url: https://github.com/Roblox/sentinel
tags: [contrastive-learning, rare-class-detection, child-safety, ncmec, embedding-similarity, behavioral-pattern, real-time]
---

# Sentinel: Roblox's Open-Source Contrastive Learning Library for Detecting Rare Harmful Text in Real-Time
**Roblox** · 2025 · [source](https://github.com/Roblox/sentinel)

## Problem
Some of the most harmful text patterns — the motivating case being child grooming attempts in Roblox chat — are so rare that conventional classifiers fail on the extreme class imbalance, and message-level classification alone misses behavior that only becomes apparent across a user's history. Roblox needed high recall on these rare classes in real time.

## Approach / System design
Sentinel applies contrastive learning principles in a two-stage pipeline. Stage one scores individual observations: each text is encoded with a sentence transformer and compared against curated positive (rare-class) and negative (common-class) example embeddings; the score reflects the ratio of similarity to rare versus common examples. Stage two aggregates recent scores from a single source (user) with statistical measures — the default is skewness, which flags asymmetric score distributions indicating rare patterns hidden amid mostly normal content; alternatives include top-k mean, percentile score, softmax-weighted mean, and max. The system deliberately prioritizes recall over precision, acting as a high-recall candidate generator for downstream review. Results carry built-in explainability: per-text similarities, the contrastive components, and nearest-neighbor snippets from the index.

## Key decisions
- Contrastive embedding similarity against curated example sets instead of training a conventional classifier on imbalanced data.
- Source-level pattern aggregation over time rather than judging each message in isolation.
- Skewness as the default aggregator to surface asymmetric distributions.
- Explainability built into outputs to support human review.
- Flexible storage via smart_open (local files or S3) and pluggable aggregators.

## Stack
Python library; sentence-transformers (all-MiniLM-L6-v2 by default) and PyTorch as optional dependencies; smart_open for local/S3 storage; Docker images in GPU and CPU variants.

## Results
Over 1,000 NCMEC (National Center for Missing & Exploited Children) reports in the first few months of production deployment at Roblox.

## Takeaways
- Analyzing patterns across multiple observations from one source achieves higher recall on rare phenomena than message-level classification alone.
- For rare-class detection, embedding similarity to curated examples sidesteps the class-imbalance problem that breaks supervised classifiers.
- A high-recall candidate generator plus human review is a workable production posture for safety-critical, low-prevalence harms.
