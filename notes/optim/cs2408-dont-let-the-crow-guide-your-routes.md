---
id: cs2408
title: Don't let the crow guide your routes
company: Instacart
primary_category: optim
sub_category: routing
year: 2022
source_url: https://tech.instacart.com/dont-let-the-crow-guide-your-routes-f24c96daedba
tags: [routing, VRP, quantile regression, grocery delivery, last-mile, operations research, stochastic optimization]
---

# Don't let the crow guide your routes
**Instacart** · 2022 · [source](https://tech.instacart.com/dont-let-the-crow-guide-your-routes-f24c96daedba)

## Problem
Instacart's logistics engine solves a Vehicle Routing Problem to match customer orders with shoppers, and route quality hinges on accurate distance estimates between locations. The original approach used Haversine ("as the crow flies") distance, which showed a 33% mean absolute percentage error (e.g., measured in Orange County) and led to suboptimal batching and routing. The accurate alternative — a routing API — was too expensive to call for the billions of distance queries the VRP solver needs daily.

## Approach / System design
A hybrid distance-estimation system combining three tiers:
1. **Haversine** — fast but inaccurate (33% MAPE).
2. **Mapbox routing API** — accurate (5% MAPE) but computationally costly at billions of queries per day, so results are cached.
3. **ML prediction** — an XGBoost model trained on historical shopper GPS trip data predicts actual traversed distance, filling in whenever the Mapbox cache misses.
Serving prioritizes cached Mapbox distances and falls back to the ML prediction for gaps.

## Key decisions
- Small, cheap feature set: origin and destination latitude/longitude plus Haversine distance (5 features total), keeping inference fast enough for VRP-scale query volumes.
- XGBoost chosen over regularized linear regression and random forests after comparing error and robustness.
- GPS outlier handling: prune bad pings with heuristics and substitute cached Mapbox distances for bad outliers in training data.
- Weekly automatic retraining, matching the semi-static nature of road distances.

## Stack
XGBoost (distance model), Mapbox API with caching (ground-truth distances), historical shopper GPS traces as training data, feeding Instacart's VRP-based logistics engine.

## Results
- ML-predicted distance achieved 11% MAPE versus 33% for Haversine.
- Multi-order trip distances dropped 9% across all operating areas.
- Millions of driving miles saved annually.

## Takeaways
- For VRP at scale, the distance oracle is the bottleneck: a cheap learned approximation layered over a cached expensive-but-accurate API captures most of the accuracy at a fraction of the cost.
- Simple features and a boosted-tree model were enough — the win came from replacing a bad geometric assumption, not from model sophistication.
- Matching retraining cadence to how fast the underlying quantity changes (roads: slowly) keeps the system cheap to operate.
