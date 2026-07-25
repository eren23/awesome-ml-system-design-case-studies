---
id: cs1782
title: Category-Specific CNN for Visual-aware CTR Prediction at JD.com
company: JD.com
primary_category: ads
sub_category: ctr-prediction
year: 2020
source_url: https://arxiv.org/abs/2006.10337
tags: [computer-vision, ctr, attention, serving-acceleration]
---

# Category-Specific CNN for Visual-aware CTR Prediction at JD.com
**JD.com** · 2020 · [source](https://arxiv.org/abs/2006.10337)

## Problem
Product images carry strong signal for ad CTR prediction in e-commerce, but off-the-shelf CNNs fall short in two ways. First, they are hard to deploy in a production ad system that needs efficient training and low-latency serving. Second, CNNs built for image classification ignore the product category, so they spend capacity extracting features that are irrelevant to how users judge items within a given category.

## Approach / System design
JD.com's Category-Specific CNN (CSCNN) injects category information directly into visual feature extraction. Instead of fusing the category late (after a generic image embedding is computed), CSCNN performs early fusion: lightweight attention modules conditioned on the product category are added to each convolutional layer, steering every stage of feature extraction toward category-relevant visual patterns. The design explicitly prioritizes production constraints — training efficiency and serving latency — alongside accuracy.

## Key decisions
- Early fusion of category knowledge inside the CNN rather than late fusion after feature extraction.
- Lightweight per-convolutional-layer attention modules to keep the added cost compatible with production serving.
- Validate at production scale, not just on benchmarks, including acceleration strategies for online serving.

## Stack
A CNN backbone augmented with category-conditioned attention modules at each convolutional layer, integrated into JD.com's ad CTR prediction system serving millions of advertisers and hundreds of millions of customers.

## Results
CSCNN outperformed baselines on benchmark datasets and on a 10-billion-scale real production dataset from JD, and an online A/B test confirmed improvements over the previous production algorithms. Exact metric lifts are not given in the source abstract.

## Takeaways
Generic pretrained vision features are not the ceiling for visual-aware CTR: conditioning feature extraction on the product category, from the earliest layers, extracts the signal users actually respond to. And for industrial adoption, the serving-acceleration work is as much a part of the contribution as the architecture.
