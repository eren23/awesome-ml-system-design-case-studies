---
id: cs2337
title: "TF-GNN: Graph Neural Networks in TensorFlow"
company: Google
primary_category: graph
sub_category: gnn
year: 2022
source_url: https://arxiv.org/abs/2207.03522
tags: [gnn, graph-ml-platform, tensorflow, heterogeneous-graph, production-infrastructure, scalable-gnn, open-source]
---

# TF-GNN: Graph Neural Networks in TensorFlow
**Google** · 2022 · [source](https://arxiv.org/abs/2207.03522)

## Problem
Google needed production-grade infrastructure for ML on massive heterogeneous graphs — billions of nodes, up to trillions of edges — with multiple node and edge types. Existing frameworks like PyTorch Geometric and DGL were not designed around this scale or around heterogeneity as a first-class concept, and researchers and production developers needed different levels of abstraction from the same library.

## Approach / System design
TF-GNN is an open-source port of Google's production-internal GNN library, built bottom-up for heterogeneous graphs. Its foundation is the GraphTensor data model: a schema (GraphSchema) declares node types, edge types, and features, and graphs are represented with native TensorFlow tensors and ragged tensors, supporting batching natively. Sampling supports three regimes: distributed sampling of rooted subgraphs for billion-scale graphs, in-memory on-the-fly sampling for graphs under ~100M nodes, and no sampling for small graphs. Modeling uses a Keras message-passing API with two-step message computation (per-edge messages from source/target pairs, then pooling to receivers), generalizing Graph Networks to heterogeneous settings including edge hidden states. The library exposes four API levels — data representation, broadcast/pool operations, Keras layers, and an end-to-end orchestrator — so different user groups pick their altitude. Distributed training rides tf.distribute.Strategy with GPU/TPU support and tf.data service for input preprocessing.

## Key decisions
- Heterogeneous-first design rather than partitioning heterogeneous graphs into homogeneous pieces.
- Deep TensorFlow ecosystem integration, allowing pretrained vision/NLP models inside GNNs and reuse of deployment tooling.
- Edge-centric abstractions with edge features and hidden states, enabling models like Graph Transformers without workarounds.
- Multi-level API design serving low-code developers and researchers from the same codebase.
- Design informed by real Google production models using the internal predecessor.

## Stack
Python, TensorFlow, Keras; Apache Beam-style distributed sampling, tf.data service, tf.distribute.Strategy; deployment via TensorFlow Serving, TFLite, and SavedModel.

## Results
On OGBN-MAG, a simple MPNN built with TF-GNN and tuned via hyperparameter search reached 0.5027 (±0.0019) test accuracy with 5.89M parameters, beating the more complex Heterogeneous Graph Transformer leaderboard entry (0.4982 ±0.0046 with 26.8M parameters) — better accuracy with roughly 5x fewer parameters. Broader success is evidenced by many production models at Google using the library.

## Takeaways
- Production use cases should shape library design from inception, not as an afterthought.
- Layered APIs let one library serve everyone from low-code practitioners to researchers.
- Simple, well-tuned models can outperform architecturally complex ones.
- Distributed sampling to cloud storage plus asynchronous training tolerates machine failures better than synchronous partitioning at extreme scale.
- Real-world graphs are heterogeneous; native support beats retrofitting.
