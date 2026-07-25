---
id: cs2131
title: "GoSage: Heterogeneous Graph Neural Network Using Hierarchical Attention for Collusion Fraud Detection"
company: Gojek
primary_category: graph
sub_category: gnn
year: 2023
source_url: https://dl.acm.org/doi/10.1145/3604237.3626856
tags: [gnn, fraud-detection, heterogeneous-graph, collusion, hierarchical-attention, food-delivery]
---

# GoSage: Heterogeneous Graph Neural Network Using Hierarchical Attention for Collusion Fraud Detection
**Gojek** · 2023 · [source](https://dl.acm.org/doi/10.1145/3604237.3626856)

## Problem
Collusion fraud on Gojek's service and payment network involves coordinated rings of customers and merchants rather than isolated bad actors. Detecting it requires modeling a heterogeneous graph where nodes are connected by multiple relation types — transactions, shared devices, and other links — which standard homogeneous GNNs handle poorly.

## Approach / System design
GoSage is a multi-level (hierarchical) attention-based heterogeneous GNN deployed at Gojek. It represents customers and merchants as nodes joined by multiple relation types and applies attention at both the node level and the relation level, so the model learns which neighbors and which relationship types matter for a given prediction. Training is semi-supervised, letting scarce fraud labels propagate through the graph structure to flag collusive patterns.

## Key decisions
- Model the problem as a heterogeneous multi-relational graph (transactions, shared devices, etc.) instead of flat tabular features.
- Hierarchical attention to capture both inter-node and inter-relational dependencies.
- Semi-supervised training to cope with limited fraud labels at industrial scale.

## Stack
Not covered in the source beyond the GNN framework itself; the paper was published at the International Conference on AI in Finance (ICAIF) 2023.

## Results
The paper reports superior performance compared to existing GNN approaches at industrial scale; specific metrics are not covered in the accessible source.

## Takeaways
Collusion fraud is fundamentally a graph problem: hierarchical attention over a heterogeneous customer–merchant graph surfaces coordinated fraud syndicates that per-entity models miss, and semi-supervision makes it workable with few labels.
