---
id: cs2255
title: Hierarchical Structure Sharing Empowers Multi-task Heterogeneous GNNs for Customer Expansion
company: JD Logistics
primary_category: graph
sub_category: gnn
year: 2025
source_url: https://arxiv.org/abs/2410.22089
tags: [multi-task-learning, heterogeneous-GNN, customer-expansion, structure-sharing, KDD-2025, logistics]
---

# Hierarchical Structure Sharing Empowers Multi-task Heterogeneous GNNs for Customer Expansion
**JD Logistics** · 2025 · [source](https://arxiv.org/abs/2410.22089)

## Problem
Customer expansion in logistics — predicting which prospects will sign contracts — suffers from extreme positive-label sparsity when framed as node classification on a heterogeneous graph. Standard multi-task learning setups that pair the sparse target task with label-rich auxiliary tasks can actually hurt performance, because they fail to separate structural patterns that are shared across tasks from those that are task-specific, causing interference during heterogeneous graph aggregation.

## Approach / System design
The paper introduces StrucHIS (Structure-aware Hierarchical Information Sharing), a multi-task heterogeneous GNN framework. It decomposes the structure-learning process of a heterogeneous GNN — multi-layer, multi-relation-type aggregation — into multiple stages, and inserts an information-sharing mechanism at each stage. This staged, hierarchical sharing lets the model transfer knowledge from a label-rich auxiliary task to the sparse customer-expansion task while explicitly controlling which structural signals are shared and which stay task-specific.

## Key decisions
- Frame customer expansion as multi-task learning, pairing the label-sparse expansion task with an auxiliary task that has abundant labels.
- Share information hierarchically at each stage of graph structure learning rather than only at the representation or output level.
- Explicitly discriminate task-shared vs. task-specific structural patterns instead of treating all learned structure uniformly, mitigating negative transfer.

## Stack
Heterogeneous graph neural networks with a custom multi-task learning framework (StrucHIS); deployed in JD Logistics' production customer-expansion system. Implementation specifics beyond the model design are not covered in the source.

## Results
- 51.41% average precision improvement on a private industrial dataset and 10.52% macro-F1 gain on a public dataset over baselines.
- In production at JD Logistics: 41.67% improvement in contract-signing success rate and over 453K new orders generated within two months of deployment.

## Takeaways
For graph-based business problems with severe label imbalance, generic multi-task GNNs are not enough — building structural awareness into the sharing mechanism itself, stage by stage, is what unlocks positive transfer. The approach translated directly into large commercial gains, showing that careful negative-transfer control matters as much as model capacity.
