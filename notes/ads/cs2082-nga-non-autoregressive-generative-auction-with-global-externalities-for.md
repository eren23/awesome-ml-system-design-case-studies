---
id: cs2082
title: "NGA: Non-autoregressive Generative Auction with Global Externalities for Advertising Systems"
company: Meituan
primary_category: ads
sub_category: auction
year: 2025
source_url: https://arxiv.org/abs/2506.05685
tags: [generative-auction, non-autoregressive, global-externalities, organic-content, list-wise, A/B-testing]
---

# NGA: Non-autoregressive Generative Auction with Global Externalities for Advertising Systems
**Meituan** · 2025 · [source](https://arxiv.org/abs/2506.05685)

## Problem
Ad auctions must simultaneously maximize revenue, preserve incentive compatibility, protect user experience, and run under tight real-time latency. Learning-based auction frameworks struggle to model global externalities — how an ad's value depends on the other ads around it and on adjacent organic content — and autoregressive designs are too slow because they decode sequentially.

## Approach / System design
NGA is an end-to-end generative auction that explicitly models global externalities by jointly capturing relationships among ads and the influence of neighboring organic content on the final page. Instead of autoregressive decoding, it generates the ad sequence with non-autoregressive parallel decoding plus constraint-based strategies, and uses a multi-tower list-wise evaluator that computes rewards and payments in a unified way over the whole list rather than per item.

## Key decisions
- Model externalities globally — including organic content interleaved with ads — rather than only pairwise/adjacent ad effects.
- Choose non-autoregressive parallel decoding for serving efficiency, with constraints to keep generation valid, instead of sequential generation.
- Unify reward and payment computation in one multi-tower list-wise evaluator so allocation quality and pricing are judged on the same footing.

## Results
Extensive offline experiments plus large-scale online A/B tests on Meituan's commercial advertising platform show NGA consistently outperforming existing methods in both effectiveness and efficiency; specific metric values are not covered in the source abstract.

## Stack
Generative sequence model with non-autoregressive decoding and a multi-tower evaluator network; deployed/tested on Meituan's ad platform. Specific frameworks are not covered in the source.

## Takeaways
For generative auctions in production, decoding latency is a first-class design constraint — non-autoregressive generation makes list-wise, externality-aware auctions servable in real time, and jointly evaluating rewards and payments list-wise keeps the mechanism coherent.
