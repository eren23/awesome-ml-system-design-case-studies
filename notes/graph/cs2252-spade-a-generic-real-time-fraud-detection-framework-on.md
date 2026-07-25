---
id: cs2252
title: "Spade+: A Generic Real-Time Fraud Detection Framework on Dynamic Graphs"
company: Grab
primary_category: graph
sub_category: community-detection
year: 2024
source_url: https://ieeexplore.ieee.org/abstract/document/10510636/
tags: [fraud-detection, dynamic-graph, edge-deletion, community-detection, IEEE-TKDE, incremental-update]
---

# Spade+: A Generic Real-Time Fraud Detection Framework on Dynamic Graphs
**Grab** · 2024 · [source](https://ieeexplore.ieee.org/abstract/document/10510636/)

## Problem
Grab detects fraudster networks as dense subgraphs in transaction graphs, but prevalent dense-subgraph methods target static graphs and ignore the evolving nature of real transaction streams. The earlier Spade system handled only edge insertions; in practice Grab also needs to expire outdated transactions — persistently adding edges without any deletion mechanism can gradually make legitimate communities look densely connected and trigger false positives.

## Approach / System design
Spade+ generalizes Spade to fully dynamic graphs, defined by an initial graph plus an update stream of both edge insertions and edge deletions. It incrementally maintains dense-subgraph (fraud community) detection results under both kinds of updates, keeping detection real time as the transaction graph evolves in production.

## Key decisions
- Support edge deletions as first-class updates, not just insertions, so stale transactions can be removed and legitimate communities don't accumulate spurious density.
- Keep the generic, incremental framework design of Spade while extending it to the fully dynamic setting.

## Stack
Incremental dense-subgraph maintenance on dynamic transaction graphs, extending Grab's Spade framework. Published in IEEE Transactions on Knowledge and Data Engineering (2024).

## Results
Not covered in the source.

## Takeaways
Real production graphs are not insert-only: transaction expiry matters, because without deletions the graph's density drifts and legitimate communities start resembling fraud rings. Extending incremental detection to handle deletions is what makes the framework generic enough for sustained real-time operation.
