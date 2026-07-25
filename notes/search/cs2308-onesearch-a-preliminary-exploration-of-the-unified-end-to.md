---
id: cs2308
title: "OneSearch: A Preliminary Exploration of the Unified End-to-End Generative Framework for E-commerce Search"
company: JD.com
primary_category: search
sub_category: retrieval
year: 2025
source_url: https://arxiv.org/abs/2509.03236
tags: [generative-retrieval, end-to-end, e-commerce, user-behavior, cascade-pipeline, arxiv-2025]
---

# OneSearch: A Preliminary Exploration of the Unified End-to-End Generative Framework for E-commerce Search
**JD.com** · 2025 · [source](https://arxiv.org/abs/2509.03236)

## Problem
Traditional e-commerce search runs as a multi-stage cascade (recall → pre-rank → rank → re-rank). Computation is fragmented across stages and each stage optimizes its own objective, so the objectives collide and cap the end-to-end performance ceiling.

## Approach / System design
OneSearch is described as the first industrially deployed end-to-end generative framework for e-commerce search, replacing the cascade with a single generative model. Three components carry the design: (1) Keyword-enhanced Hierarchical Quantization Encoding (KHQE), which builds semantic item identifiers that preserve hierarchical semantics and distinctive item attributes while keeping query-item relevance constraints; (2) multi-view user behavior sequence injection, which constructs behavior-driven user IDs from both explicit short-term and implicit long-term behavior sequences to personalize generation; and (3) a Preference-Aware Reward System (PARS) that applies multi-stage supervised fine-tuning followed by adaptive reward-weighted ranking to align outputs with user preference. The system is deployed across multiple search scenarios serving millions of users and tens of millions of daily page views.

## Key decisions
- Collapse the cascade into one generative model to remove cross-stage objective conflicts and fragmented compute.
- Encode items with keyword-enhanced hierarchical quantization rather than plain codebook IDs, keeping relevance constraints intact in the generative ID space.
- Inject multi-view (short-term explicit + long-term implicit) behavior sequences as user identity signals for personalization.
- Align the generator with a reward system (SFT stages plus adaptive reward-weighted ranking) instead of relying on likelihood training alone.

## Stack
Generative retrieval model with hierarchical quantization encoding (KHQE), behavior-driven user ID construction, and a preference-aware reward pipeline (multi-stage SFT + reward-weighted ranking). Further serving details are not covered in the source.

## Results
- Item CTR +1.67%, buyer conversion +2.40%, order volume +3.22% in deployment.
- Operational expenditure reduced by 75.40%.
- Model FLOPs Utilization improved from 3.26% to 27.32%.

## Takeaways
A single end-to-end generative model can beat a tuned cascade on both business metrics and efficiency: removing stage boundaries eliminates objective collisions, and dense generative computation uses hardware far better (8x MFU) while cutting serving cost dramatically.
