---
id: cs2167
title: "IDProxy: Cold-Start CTR Prediction for Ads and Recommendation at Xiaohongshu with Multimodal LLMs"
company: Xiaohongshu
primary_category: ads
sub_category: ctr-prediction
year: 2026
source_url: https://arxiv.org/abs/2603.01590
tags: [cold-start, multimodal-llm, ctr-prediction, content-feed, display-ads, item-id-proxy]
---

# IDProxy: Cold-Start CTR Prediction for Ads and Recommendation at Xiaohongshu with Multimodal LLMs
**Xiaohongshu** · 2026 · [source](https://arxiv.org/abs/2603.01590)

## Problem
CTR models in ads and recommendation rely heavily on item ID embeddings, which are learned from historical interactions. New items have no such history, so ID embeddings fail in cold-start settings — a structural gap for a content platform where fresh items arrive constantly.

## Approach / System design
IDProxy uses multimodal LLMs to generate proxy embeddings for new items from their content signals (rather than behavior). The proxies are explicitly aligned with the existing ID embedding space, so the ranking model can consume them as drop-in stand-ins for learned ID embeddings. The whole path is optimized end-to-end with the CTR objective alongside the ranking model, and integrates into Xiaohongshu's large-scale ranking pipelines. Deployed in the Explore Feed across both Content Feed and Display Ads, serving hundreds of millions of daily users.

## Key decisions
- Derive cold-start representations from content via multimodal LLMs instead of waiting for behavioral data to accumulate.
- Align proxy embeddings with the existing ID embedding space rather than introducing a separate cold-start feature path — no ranking-model surgery required.
- Train the proxy generation end-to-end against CTR objectives so proxies are optimized for the actual ranking task, not just semantic similarity.

## Stack
Multimodal LLMs for content encoding, integrated with Xiaohongshu's production CTR ranking pipelines for Content Feed and Display Ads.

## Results
Offline experiments and online A/B tests demonstrated effectiveness per the source abstract; the catalog records a +1.93% Advertiser Value gain. No other numbers stated in the source.

## Takeaways
The cold-start fix that ships is the one that respects the existing system: by aligning MLLM-derived content embeddings to the live ID embedding space and training against the CTR objective, new items get useful representations from day one without rearchitecting the ranker.
