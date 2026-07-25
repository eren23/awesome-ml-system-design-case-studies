---
id: cs2129
title: "RankGraph-2: Lifecycle Co-Design for Billion-Node Graph Learning in Recommendation"
company: Meta
primary_category: graph
sub_category: gnn
year: 2026
source_url: https://arxiv.org/abs/2606.18379
tags: [gnn, recommendation-retrieval, billion-scale, lifecycle-co-design, knn, graph-construction]
---

# RankGraph-2: Lifecycle Co-Design for Billion-Node Graph Learning in Recommendation
**Meta** · 2026 · [source](https://arxiv.org/abs/2606.18379)

## Problem
Billion-node graph-based retrieval requires solving graph construction, representation learning, and real-time serving together. Treating the three stages independently — the traditional approach — produces inefficiencies and suboptimal end-to-end results, especially for similarity retrieval tasks like U2U2I and U2I2I.

## Approach / System design
RankGraph-2 co-designs the full lifecycle so each stage's constraints shape the others. Construction reduces hundreds of trillions of candidate edges to hundreds of billions via subsampling with popularity-bias correction. Learning pre-computes multi-hop neighborhoods with personalized PageRank, avoiding online graph traversal. Serving co-learns a residual-quantization cluster index during training, so retrieval hits a compact index instead of running expensive online KNN.

## Key decisions
- Make all serving data self-contained and pre-computed, eliminating the need for online graph infrastructure.
- Bake the cluster index into the training objective (index co-training) so learned representations satisfy serving constraints by construction.
- Support hour-level refresh cycles for item coverage/freshness.

## Stack
Not covered in the source beyond the framework itself (personalized PageRank precomputation, residual-quantization cluster indexing).

## Results
83% reduction in serving computational cost; 3.8x higher recall than GAT + Deep Graph Infomax on bipartite graphs and 2.1x higher than PyTorch-BigGraph on item retrieval; +0.96% CTR and +2.75% CVR in A/B tests; powers 20+ retrieval launches across major surfaces.

## Takeaways
At billion-node scale, the win comes from coupling construction, training, and serving into one designed lifecycle — isolated per-stage optimization leaves both quality and infrastructure cost on the table.
