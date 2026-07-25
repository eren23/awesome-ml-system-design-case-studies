---
id: cs2080
title: "EGA-V2: An End-to-end Generative Framework for Industrial Advertising"
company: Meituan
primary_category: ads
sub_category: auction
year: 2025
source_url: https://arxiv.org/abs/2505.17549
tags: [generative-model, end-to-end, ad-allocation, creative-selection, payment-optimization, cascaded-system]
---

# EGA-V2: An End-to-end Generative Framework for Industrial Advertising
**Meituan** · 2025 · [source](https://arxiv.org/abs/2505.17549)

## Problem
Multi-stage cascaded ad architectures prune promising candidates too early and fragment decisions (retrieval, ranking, creative, allocation, pricing) across disconnected modules with inconsistent objectives. Existing generative recommendation approaches skip the parts that make advertising real: explicit bidding, creative selection, ad allocation, and payment computation.

## Approach / System design
EGA-V2 is a single unified generative model that jointly handles user interest modeling, POI (point-of-interest) and creative generation, ad allocation, and payment optimization end-to-end. It uses hierarchical tokenization with multi-token prediction to generate POI recommendations and ad creatives jointly; a permutation-aware reward model to align user experience with advertiser objectives; a token-level bidding strategy for explicit bid generation; and a differentiable ex-post regret minimization mechanism that decouples allocation from payment while keeping approximate incentive compatibility at the POI level.

## Key decisions
- Replace cascaded filtering with end-to-end generation so promising candidates aren't discarded by early stages.
- Model auction economics inside the generative model (token-level bids, payment mechanism) rather than bolting an auction on afterwards.
- Decouple allocation from payment via differentiable regret minimization to satisfy auction-theoretic requirements (approximate incentive compatibility) in a learned system.
- Use permutation-aware rewards so the generated list balances user experience against advertiser value.

## Stack
Autoregressive/generative architecture with hierarchical tokenization and multi-token prediction, a reward model, and a differentiable payment mechanism. Evaluated on large-scale real traffic data from Meituan's advertising platform (the manifest cites 200M real requests). Specific frameworks are not covered in the source.

## Results
Offline evaluations show EGA-V2 significantly outperforms traditional cascaded systems in both performance and practicality; specific quantitative metrics are not covered in the source abstract.

## Takeaways
Positioned as the first fully generative framework covering the complete industrial ad workflow — the interesting part is not just generation replacing ranking, but embedding bidding, allocation, and incentive-compatible payments into the generative model itself.
