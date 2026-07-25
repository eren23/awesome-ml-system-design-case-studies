---
id: cs1783
title: Truncation-Free Matching System for Display Advertising at Alibaba
company: Alibaba
primary_category: ads
sub_category: targeting
year: 2021
source_url: https://arxiv.org/abs/2102.09283
tags: [ad-matching, retrieval, near-line, truncation]
---

# Truncation-Free Matching System for Display Advertising at Alibaba
**Alibaba** · 2021 · [source](https://arxiv.org/abs/2102.09283)

## Problem
Alibaba's display advertising matching stage runs a two-step pipeline — identify the user crowds a request belongs to, then retrieve the ads targeting those crowds. Under online latency constraints the long tail of results has to be truncated, so not all eligible ads get a chance to participate in matching. That truncation silently drops valuable candidates, hurting ad delivery for advertisers and costing the platform revenue.

## Approach / System design
The fix is architectural rather than model-side: decouple the matching computation from the latency-sensitive serving path. A near-line system pre-calculates, truncation-free, the top valuable ads for each user and stores them; the online path then simply fetches the pre-computed result when a request arrives. Because the heavy matching work happens near-line with no per-request latency budget, no candidate needs to be cut for time.

## Key decisions
- Move matching out of the request path entirely — near-line pre-calculation instead of online computation.
- Pre-compute and store the top valuable ads per user so online serving reduces to a lookup.
- Separate the system into a batch/near-line component and a lightweight online serving component with distinct constraints.

## Stack
A near-line pre-calculation and storage system feeding Alibaba's online display-ad serving. Specific storage and compute technologies are not covered in the source.

## Results
Deployed in Alibaba's production system since 2019. Advertisers previously affected by truncation saw more than a 50% improvement in impressions, and the platform gained 9.4% in Revenue Per Mille (RPM) — described as significant for the business.

## Takeaways
When latency budgets force lossy truncation, the answer can be to change where the work happens, not to build a better model. Pre-computing exhaustive matching results near-line removes the truncation loss entirely while keeping online serving fast, and the impression and RPM gains show how much value truncation had been leaving on the table.
