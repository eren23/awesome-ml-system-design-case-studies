---
id: cs2175
title: "LiDDA: Data Driven Attribution at LinkedIn"
company: LinkedIn
primary_category: ads
sub_category: attribution
year: 2025
source_url: https://arxiv.org/abs/2505.09861
tags: [multi-touch-attribution, transformer, data-driven, advertising-measurement, member-level, aggregate-level]
---

# LiDDA: Data Driven Attribution at LinkedIn
**LinkedIn** · 2025 · [source](https://arxiv.org/abs/2505.09861)

## Problem
Attribution — deciding which marketing touchpoints deserve credit for a conversion — underpins LinkedIn's advertising platform, but the signals live at different granularities: individual member interactions, aggregate-level metrics, and external macro factors. LinkedIn needed one scalable system that could reason over all of them.

## Approach / System design
LiDDA is a unified transformer-based data-driven attribution model deployed at production scale. The transformer ingests sequential marketing interactions and merges three data categories into a single framework: member-level interaction sequences, aggregate-level signals, and external market variables. The same architecture serves attribution from individual-member granularity up to platform-wide measurement.

## Key decisions
- Transformer architecture chosen for modeling ordered sequences of marketing touchpoints.
- One unified model across heterogeneous data granularities instead of separate member-level and aggregate-level attribution systems.
- Explicit incorporation of external macro factors so credit assignment isn't confounded by market-wide shifts.

## Stack
Transformer neural network deployed on LinkedIn's large-scale production infrastructure; heterogeneous data-integration pipeline. No further tooling named in the source.

## Results
The source describes significant production impact but states no specific numeric metrics.

## Takeaways
A single transformer over mixed-granularity signals can replace fragmented attribution heuristics; the authors position the design and its lessons as broadly applicable across marketing and ad-tech, suggesting unified sequence models are a generalizable pattern for attribution.
