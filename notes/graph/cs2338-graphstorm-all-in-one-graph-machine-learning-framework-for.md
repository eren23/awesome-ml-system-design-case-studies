---
id: cs2338
title: "GraphStorm: All-in-one Graph Machine Learning Framework for Industry Applications"
company: Amazon
primary_category: graph
sub_category: gnn
year: 2024
source_url: https://arxiv.org/abs/2406.06022
tags: [gnn, graph-ml-platform, enterprise-gnn, distributed-training, billion-scale, scalable-gnn, aws, kdd]
---

# GraphStorm: All-in-one Graph Machine Learning Framework for Industry Applications
**Amazon** · 2024 · [source](https://arxiv.org/abs/2406.06022)

## Problem
Industry adoption of graph ML is blocked by three barriers: graphs at massive scale (millions to billions of nodes and edges), complex heterogeneous structures with diverse feature types, and source data living in non-graph formats (tables) that must be transformed and partitioned before any GNN can train. Teams need both accessibility for non-experts and depth for advanced users.

## Approach / System design
GraphStorm is an end-to-end framework covering scalable graph construction, model training, and inference, operable via single commands. The construction pipeline turns tabular data (CSV, Parquet) into a distributed graph format through feature transformation, ID mapping, and distributed partitioning with edge-cut algorithms (random, METIS). Models are split into three composable parts — node/edge input encoders, GNN graph encoders, and task decoders — supporting node-, edge-, and graph-level tasks. The distributed engine builds on DistDGL with on-the-fly mini-batch sampling across clusters and unified CPU/GPU interfaces. A model zoo covers RGCN, RGAT, and HGT for heterogeneous graphs; GCN, GAT, and GraphSage for homogeneous; TGAT for temporal; and LM+GNN combinations for text-rich graphs.

## Key decisions
- On-the-fly sampling rather than preprocessed samples, keeping hyperparameter experimentation flexible.
- No-code/low-code split: command-line interface for prototyping, custom APIs for advanced users.
- Modular architecture supporting multi-task learning, LM-GNN co-training, and EM-style training strategies.
- Dedicated link-prediction dataloader with multiple negative sampling methods (uniform, joint, in-batch).
- Layered abstractions (engine → pipelines → models → UI) so scale needs no user code changes.

## Stack
Python on DGL/DistDGL and PyTorch, Spark integration for distributed processing, Amazon SageMaker deployment support; open-sourced as awslabs/graphstorm.

## Results
Microsoft Academic Graph (484M nodes, 7.5B edges): data processing plus model training within hours. Synthetic benchmarks: a 1B-edge graph takes 19 min preprocessing and 1.5 min per-epoch training on 8 instances; a 100B-edge graph takes 61 min preprocessing and 50 min training on 32 instances. Fine-tuned BERT+GNN improved over pre-trained embeddings by 11–40% on node and link prediction tasks; GNN distillation lifted DistilBERT by 8.2%; graph schema refinement alone gave a 15% improvement without architecture changes. Deployed in over a dozen billion-scale industry applications since its May 2023 release.

## Takeaways
- Layered abstraction lets one framework serve both single-command users and researchers at billion-edge scale.
- Modeling flexibility (schema experimentation, LM fine-tuning strategy) delivers gains comparable to architecture changes.
- Negative sampling strategy is critical to balancing efficiency and quality in link prediction.
- Production deployment across many billion-scale applications validates the design.
