---
id: cs2278
title: Real-Time Intelligent Dispatching Algorithms Build the World's Largest Minute-Level Delivery Network
company: Meituan
primary_category: optim
sub_category: dispatch
year: 2024
source_url: https://pubsonline.informs.org/doi/10.1287/inte.2023.0084
tags: [real-time-dispatch, reinforcement-learning, courier-routing, on-demand-delivery, large-scale, informs]
---

# Real-Time Intelligent Dispatching Algorithms Build the World's Largest Minute-Level Delivery Network
**Meituan** · 2024 · [source](https://pubsonline.informs.org/doi/10.1287/inte.2023.0084)

## Problem
Meituan runs the world's largest minute-level delivery network: 60M+ orders per day dispatched to 5M+ couriers. Assigning orders to couriers in real time is an NP-hard combinatorial problem under dynamic, uncertain conditions (traffic, meal prep times, courier positions) that must be solved in seconds while honoring customer delivery promises and keeping courier workloads reasonable.

## Approach / System design
A dispatching system that fuses operations research with machine learning:
- Graph representation learning to encode the delivery network structure.
- Inverse reinforcement learning to infer the objectives that good dispatch decisions optimize.
- Multiobjective optimization balancing customer satisfaction, courier workload, and network efficiency.
- Real-time combinatorial algorithms producing high-quality assignments within seconds at full scale.

## Key decisions
- Hybridize classical combinatorial optimization with ML rather than relying on pure heuristics or pure learning — mathematical structure for solution quality, learning for the environment's uncertainty.
- Engineer for seconds-level solve times without sacrificing solution quality, since millions of simultaneous assignments depend on it.
- Optimize explicitly for multiple stakeholders (customers, couriers, platform) instead of a single cost objective.

## Stack
Graph representation learning, inverse reinforcement learning, multiobjective combinatorial optimization, real-time dispatch algorithms. Published in INFORMS journal (Franz Edelman competition track).

## Results
Since the post-2019 implementation:
- Average order delivery time reduced 20.96%.
- Average courier travel distance per order reduced 23.77%.
- ~$0.23 billion in annual cost savings.
- The dispatch capability enabled new business lines (Meituan Instashopping, Meituan Grocery).

## Takeaways
At extreme scale, real-time dispatch pays off only as a hybrid: OR provides rigor on the assignment problem, ML handles uncertainty and objective inference. The gains landed on both sides of the marketplace — faster deliveries for customers and shorter distances for couriers — and a strong dispatch engine became a platform asset that unlocked entirely new delivery businesses.
