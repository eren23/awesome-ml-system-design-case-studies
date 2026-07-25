---
id: cs1779
title: LightSAGE: Graph Neural Networks for Large Scale Item Retrieval in Shopee's Advertisement Recommendation
company: Shopee
primary_category: ads
sub_category: targeting
year: 2023
source_url: https://arxiv.org/abs/2310.19394
tags: [graph-neural-network, retrieval, cold-start, embeddings]
---

# LightSAGE: Graph Neural Networks for Large Scale Item Retrieval in Shopee's Advertisement Recommendation
**Shopee** · 2023 · [source](https://arxiv.org/abs/2310.19394)

## Problem
GNNs are the trending solution for item retrieval in recommendation, but most published work centers on architecture while industrial deployment hinges on other things too: how the item graph is constructed, and how to handle cold-start and long-tail items — both especially critical in an ads system, where new promoted inventory must be retrievable from day one.

## Approach / System design
Shopee's solution has three legs. First, graph construction: high-quality item graphs are built by merging strong user behavioral signals with edges derived from collaborative filtering algorithms, so the graph is dense and reliable rather than an afterthought. Second, the model: LightSAGE, a GNN architecture that produces item embeddings consumed by vector search for ad item retrieval. Third, data handling: explicit strategies for cold-start and long-tail items so sparse-history inventory still receives useful embeddings.

## Key decisions
- Treat graph construction quality and data-sparsity handling as first-class problems, on par with model architecture.
- Combine behavioral signals with collaborative filtering when building the graph, rather than relying on either alone.
- Serve retrieval through embeddings plus vector search, the standard scalable pattern for large candidate pools.
- Build dedicated mechanisms for cold-start and long-tail items, which ads systems cannot ignore.

## Stack
LightSAGE GNN producing item embeddings; item graphs built from user behavior signals and collaborative filtering; vector search for online retrieval; deployed in Shopee's recommendation advertisement system.

## Results
The models improved offline evaluations and online A/B tests, and were deployed to the main traffic of Shopee's Recommendation Advertisement system. The source abstract does not quantify the lifts.

## Takeaways
Industrial GNN retrieval succeeds or fails on the unglamorous parts: the quality of the graph you build and how you treat items with little or no history. Shopee's framing — graph construction, model, and sparsity handling as equal pillars — is a useful checklist for anyone porting academic GNN work into a production ads retrieval stack.
