---
id: cs0860
title: Evolution of Ads Conversion Optimization Models at Pinterest
company: Pinterest
primary_category: ads
sub_category: ctr-prediction
year: 2024
source_url: https://medium.com/pinterest-engineering/evolution-of-ads-conversion-optimization-models-at-pinterest-84b244043d51
tags: [ad ranking, targeting]
---

# Evolution of Ads Conversion Optimization Models at Pinterest
**Pinterest** · 2024 · [source](https://medium.com/pinterest-engineering/evolution-of-ads-conversion-optimization-models-at-pinterest-84b244043d51)

## Problem
Predicting ad conversions (checkout, add-to-cart, etc.) is harder than predicting clicks: conversion labels are sparse, feedback is delayed with a long-tail distribution, and label quality varies because conversions are reported by advertiser platforms. Pinterest needed to keep improving conversion prediction at the scale of hundreds of millions of users and billions of items.

## Approach / System design
A multi-year architectural evolution:
- 2018: GBDT models acting as feature transformers feeding logistic regression, with feature hashing to manage sparse advertiser-ID spaces.
- 2020: Move to deep learning with multi-task learning, co-training multiple objectives (clicks, checkouts, add-to-cart).
- 2021–2023: AutoML for automated feature engineering, a unified ML platform (MLEnv), and ensemble architectures combining multiple feature-interaction backbones.

## Key decisions
- Feature-interaction modules progressed from plain MLP to DCNv2, Transformer self-attention, and MaskNet (instance-guided masking).
- Multi-task learning plus ensembling: a shared bottom for feature processing with separated top architectures; ensemble of DCNv2 and Transformer backbones (DHEN-style).
- User sequence modeling with long lookback windows to capture sparse interactions and shifting interests.
- GPU serving migration using CUDA Graphs (cut kernel-launch overhead) and mixed-precision (FP32/FP16) inference to reduce latency and memory.

## Stack
PyTorch, CUDA Graphs, mixed-precision inference, DHEN-style deep/hierarchical ensembles, sequence Transformers, AutoML, MLEnv platform.

## Results
The source reports meaningful offline and online metric gains across the iterations but does not disclose specific quantitative figures.

## Takeaways
Conversion optimization is a long iterative arc rather than one model: the wins compound from better feature interactions, multi-task/ensemble modeling, user-sequence features, and serving-efficiency work (GPU + CUDA Graphs + mixed precision) that makes the larger models affordable to serve.
