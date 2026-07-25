---
id: cs2081
title: Generative Bid Shading in Real-Time Bidding Advertising
company: Meituan
primary_category: ads
sub_category: bidding
year: 2025
source_url: https://arxiv.org/abs/2508.06550
tags: [bid-shading, generative-model, autoregressive, real-time-bidding, reward-alignment, DSP]
---

# Generative Bid Shading in Real-Time Bidding Advertising
**Meituan** · 2025 · [source](https://arxiv.org/abs/2508.06550)

## Problem
Standard bid shading in first-price RTB uses two-stage pipelines (win-rate estimation, then ratio optimization) that assume unimodal surplus curves, accumulate cascading errors between stages, ignore dependencies between discretized bid intervals, and suffer sample selection bias from only observing outcomes of placed bids.

## Approach / System design
GBS (Generative Bid Shading) replaces the two-stage pipeline with two components. First, an autoregressive generative model produces the shading ratio via stepwise residual generation, capturing dependencies across value levels without assuming a surplus-curve shape. Second, a reward alignment system tunes the generator: CHNet, a channel-aware hierarchical dynamic network, serves as the reward model, complemented by surplus optimization and exploration utility modules, with group relative policy optimization (GRPO) balancing short-term and long-term surplus.

## Key decisions
- Go end-to-end generative instead of two-stage win-rate-then-optimize, eliminating cascading errors and unimodality assumptions.
- Generate ratios as stepwise residuals so inter-interval dependencies are modeled explicitly.
- Use a hierarchical, channel-aware reward network (CHNet) for fine-grained feature extraction across ad channels.
- Optimize with GRPO against a dual objective (immediate surplus vs. long-term exploration/learning value).

## Stack
Autoregressive generative model plus a reward-model-driven alignment loop (CHNet + GRPO), deployed on Meituan's DSP. Specific serving infrastructure is not covered in the source.

## Results
Validated in offline experiments and online A/B tests; deployed in production on the Meituan DSP serving billions of bid requests daily. Specific lift numbers are not covered in the source abstract.

## Takeaways
Bid shading can be treated as a generation-plus-alignment problem: an autoregressive generator sidesteps the structural assumptions of classic surplus-curve methods, and LLM-style preference optimization (GRPO with a learned reward model) works for aligning auction actions, not just text.
