---
id: cs2254
title: "JPEC: A Novel Graph Neural Network for Competitor Retrieval in Financial Knowledge Graphs"
company: JPMorgan Chase
primary_category: graph
sub_category: gnn
year: 2024
source_url: https://arxiv.org/abs/2411.02692
tags: [financial-knowledge-graph, competitor-retrieval, GNN, link-prediction, SIGIR-2024, node-proximity]
---

# JPEC: A Novel Graph Neural Network for Competitor Retrieval in Financial Knowledge Graphs
**JPMorgan Chase** · 2024 · [source](https://arxiv.org/abs/2411.02692)

## Problem
Retrieving competitors of a given company from a financial knowledge graph is hard: the graph mixes directed and undirected relationship types, nodes carry attributes, and annotated competitor links are sparse. Existing state-of-the-art graph models handle these characteristics poorly, and manual competitor identification by analysts does not scale.

## Approach / System design
JPMorgan built JPEC (JPMorgan Proximity Embedding for Competitor detection), a graph neural network that learns embeddings capturing both first-order proximity (direct connections) and second-order proximity (shared neighborhoods), combined with important node features. Framing competitor identification as a retrieval/link-prediction task over the knowledge graph lets the model surface competitor relationships that are not explicitly annotated.

## Key decisions
- Model multi-order proximity (first- and second-order) jointly rather than relying only on direct edges, which addresses the sparsity of labeled competitor links.
- Design the architecture to accommodate the heterogeneity of the financial knowledge graph: attributed nodes and mixed directed/undirected relations.
- Combine structural proximity signals with vital node features rather than using structure alone.

## Stack
Graph neural networks and graph embedding techniques over JPMorgan's internal financial knowledge graph. Published at SIGIR 2024. Specific frameworks and serving infrastructure are not covered in the source.

## Results
JPEC outperformed most existing models in extensive competitor-retrieval experiments. The catalog entry notes it outperformed human expert predictions on competitor identification. Specific quantitative metrics are not covered in the source abstract.

## Takeaways
When labels are sparse, encoding relationship context beyond immediate neighbors — second-order proximity — meaningfully improves retrieval in knowledge graphs. Financial-domain graphs need architectures built for heterogeneous, attributed, mixed-direction edges rather than off-the-shelf GNNs.
