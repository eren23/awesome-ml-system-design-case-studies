---
id: cs2351
title: "TwERC: High Performance Ensembled Candidate Generation for Ads Recommendation at Twitter"
company: Twitter
primary_category: rec
sub_category: candidate-generation
year: 2023
source_url: https://arxiv.org/abs/2302.13915
tags: [ensemble, candidate-generation, ads-recommendation, two-tower, ann-search, high-performance]
---

# TwERC: High Performance Ensembled Candidate Generation for Ads Recommendation at Twitter
**Twitter** · 2023 · [source](https://arxiv.org/abs/2302.13915)

## Problem
The candidate generation stage of Twitter's ads recommendation funnel must feed high-quality candidates to downstream ranking while staying computationally cheap. A single retrieval strategy has blind spots, and industrial candidate generation involves complex product trade-offs that simple engagement metrics fail to capture.

## Approach / System design
TwERC is a machine-learning-first heterogeneous re-architecture of ads candidate generation. It combines a real-time light ranker with two complementary sourcing strategies that surface signals the light ranker misses. The first strategy leverages similarity signals from the interaction graph to find relevant ad candidates. The second caches and reuses ranking scores computed in earlier stages ("RankScore caching") to resurface high-potential candidates. The strategies are ensembled because their biases are complementary — each covers blind spots of the light ranker and of the other strategy.

## Key decisions
- Ensemble multiple heterogeneous retrieval strategies instead of betting on a single candidate source.
- Pair a real-time light ranker with graph-based similarity retrieval and score-caching retrieval, chosen for complementary bias profiles.
- Introduce a dedicated set of metrics for candidate generation that captures the multi-dimensional product trade-offs of the funnel, rather than relying only on downstream engagement metrics.

## Stack
Not covered in the source beyond the system components (light ranker, graph-based sourcing, score cache).

## Results
The graph-based strategy delivered a 4.08% revenue gain and the RankScore caching strategy a 1.38% revenue gain; combined, the ensemble reached roughly 5.5% revenue improvement.

## Takeaways
In mature ads funnels, candidate generation still holds substantial headroom: ensembling retrieval strategies with deliberately different biases yields additive revenue gains. Measuring candidate generation with purpose-built metrics, rather than end-of-funnel engagement alone, is necessary to reason about those trade-offs.
