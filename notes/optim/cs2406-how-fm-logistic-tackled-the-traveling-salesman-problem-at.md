---
id: cs2406
title: How FM Logistic tackled the traveling salesman problem at warehouse scale with AlphaEvolve
company: FM Logistic
primary_category: optim
sub_category: routing
year: 2026
source_url: https://cloud.google.com/blog/products/ai-machine-learning/how-fm-logistic-tackled-the-traveling-salesman-problem-at-warehouse-scale-with-alphaevolve
tags: [routing, warehouse, AlphaEvolve, evolutionary optimization, TSP, Gemini, last-mile]
---

# How FM Logistic tackled the traveling salesman problem at warehouse scale with AlphaEvolve
**FM Logistic** · 2026 · [source](https://cloud.google.com/blog/products/ai-machine-learning/how-fm-logistic-tackled-the-traveling-salesman-problem-at-warehouse-scale-with-alphaevolve)

## Problem
FM Logistic's Polish warehouse — the size of 8 football fields with 17,700+ picking locations — has dozens of operators on electric trucks navigating storage locations daily, a traveling-salesman problem at scale. Every inefficient step compounds into lost time, fleet wear, and delayed orders. The incumbent greedy routing algorithm optimized locally per route and could not coordinate picking routes globally.

## Approach / System design
FM Logistic used AlphaEvolve, Google DeepMind's Gemini-powered evolutionary coding agent. The existing step-by-step routing algorithm served as the seed; AlphaEvolve generated thousands of mutated code variants and iteratively refined them via automated evaluation against real warehouse data, producing human-readable candidate algorithms. Evaluation ran on a dataset of 60 representative tours (about an hour of workforce data), with average travel distance per pick as the primary metric and penalties for operational violations: forklift capacity breaches, missed pending orders, duplicate box assignments, FIFO priority violations, and exceeding real-time computation limits.

## Key decisions
- Seed with the human-designed baseline rather than evolving from scratch — domain expertise anchors the search.
- Build a custom evaluation function encoding real operational constraints as penalties, so evolved algorithms are deployable, not just fast on paper.
- Enforce real-time computation limits inside the evaluation so winners fit production latency budgets.
- Require interpretable output so operations teams can understand and trust the discovered routing logic.

## Stack
AlphaEvolve (Google DeepMind), Gemini models for code generation and refinement, Google Cloud for platform and compute.

## Results
- 10.4% routing-efficiency improvement over the previous best algorithm — on an already heavily optimized baseline.
- More than 15,000 fewer kilometers traveled per year in the warehouse.
- The winning algorithm introduced three improvements: density-based anchor selection (clusters of nearby items as route starting points), two-stage filtering (quick filter then precise distance simulation to stay real-time), and flexible route building (returning ill-fitting orders to the pool instead of forcing them into suboptimal routes).
- Operational impact: same-size teams handle larger volumes, faster fulfillment, less fleet wear, better operator conditions.

## Takeaways
- Evolutionary AI can out-design manual engineering on mature combinatorial problems while keeping solutions interpretable.
- Encoding failure modes (capacity, FIFO, latency) as evaluation penalties is what separates deployable algorithms from benchmark winners.
- A pilot in one Polish warehouse is extending to other facilities, with road transport and broader supply chain optimization as next candidates.
