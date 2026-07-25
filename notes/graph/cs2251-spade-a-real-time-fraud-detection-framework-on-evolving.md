---
id: cs2251
title: "Spade: A Real-Time Fraud Detection Framework on Evolving Graphs"
company: Grab
primary_category: graph
sub_category: fraud-rings
year: 2022
source_url: https://dl.acm.org/doi/10.14778/3570690.3570696
tags: [fraud-detection, dense-subgraph, dynamic-graph, incremental-update, community-detection, VLDB-2022, real-time]
---

# Spade: A Real-Time Fraud Detection Framework on Evolving Graphs
**Grab** · 2022 · [source](https://dl.acm.org/doi/10.14778/3570690.3570696)

## Problem
Financial and e-commerce platforms need to catch fraud rings in real time. Fraud communities show up as dense subgraphs in transaction graphs, but existing dense-subgraph detection methods assume static graphs — recomputing detection from scratch on every update is computationally prohibitive for a transaction network that changes constantly.

## Approach / System design
Spade is an incremental fraud detection framework that maintains dense subgraphs as the transaction graph evolves, rather than recomputing them per update. It builds on peeling-style dense-subgraph algorithms and automatically incrementalizes them, so detection results stay current as edges stream in. Developers plug in custom suspiciousness functions defining their fraud semantics, and the framework handles the incremental maintenance; edge grouping and batch update handling further reduce latency.

## Key decisions
- Incremental maintenance of dense subgraphs instead of full recomputation on each graph update.
- A customizable-semantics API: domain experts supply suspiciousness functions and Spade incrementalizes the resulting peeling algorithm automatically.
- Batch updates and edge grouping to keep per-update latency low.

## Stack
Graph-based anomaly detection with incremental peeling algorithms on evolving transaction graphs; deployed in the context of Grab's fraud detection. Published in PVLDB Vol. 16 (VLDB 2022).

## Results
Detects fraudulent communities in hundreds of microseconds on million-scale graphs; incrementalized algorithms run up to a million times faster than their static counterparts.

## Takeaways
Incrementalizing static dense-subgraph algorithms is what makes graph-based fraud-ring detection production-viable in real time. Separating fraud semantics (expert-defined suspiciousness functions) from the maintenance machinery lets domain experts adapt detection logic without reimplementing algorithms.
