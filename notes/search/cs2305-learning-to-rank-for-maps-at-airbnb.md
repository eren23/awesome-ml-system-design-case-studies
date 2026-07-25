---
id: cs2305
title: Learning to Rank for Maps at Airbnb
company: Airbnb
primary_category: search
sub_category: learning-to-rank
year: 2024
source_url: https://arxiv.org/abs/2407.00091
tags: [learning-to-rank, maps, user-interaction, kdd-2024, arxiv-2024]
---

# Learning to Rank for Maps at Airbnb
**Airbnb** · 2024 · [source](https://arxiv.org/abs/2407.00091)

## Problem
Airbnb shows search results through two very different interfaces: list-results (rectangular cards with images, prices, and ratings) and map-results (oval price pins on a map). Both historically used the same booking-probability-based ranking algorithm, but the basic assumptions underlying list ranking — built for a world of sequentially scanned lists — break down when results are presented spatially on a map, where users scan and interact in a fundamentally different way.

## Approach / System design
The team revisited the mathematical foundations of how user interactions are modeled, rather than porting list-ranking machinery onto the map. Through an iterative, experiment-driven process they developed ranking strategies tailored to each interface's interaction patterns, ultimately arriving at a unified theory covering both list and map presentation that accounts for how interface design changes the validity of ranking assumptions.

## Key decisions
- Reject a one-size-fits-all ranker across interfaces; model list and map user behavior separately.
- Revise the probabilistic user-interaction model itself instead of just retraining the existing model on map data.
- Validate every change through online experiments, converging on a unified theory of the two interfaces.

## Stack
Not covered in the source (the paper focuses on ranking methodology rather than infrastructure).

## Results
The changes produced one of the largest improvements in user experience in Airbnb search's history, validated experimentally. Specific numeric metrics are not stated in the source.

## Takeaways
Interface modality shapes ranking mathematics: assumptions valid for scrolled lists (e.g., positional attention) do not transfer to maps. When the presentation layer changes, the ranking objective and interaction model need to be re-derived, not just refit.
