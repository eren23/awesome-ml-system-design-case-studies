---
id: cs2253
title: Augmenting Knowledge Graph Hierarchies Using Neural Transformers
company: Adobe
primary_category: graph
sub_category: knowledge-graph
year: 2024
source_url: https://arxiv.org/abs/2404.08020
tags: [knowledge-graph, hierarchy-learning, LLM, taxonomy, content-understanding, ECIR-2024, intent-graph]
---

# Augmenting Knowledge Graph Hierarchies Using Neural Transformers
**Adobe** · 2024 · [source](https://arxiv.org/abs/2404.08020)

## Problem
Knowledge graphs often lack complete hierarchical structure, which limits their usefulness for organizing and understanding data. Adobe needed to automatically generate and augment missing hierarchies in an existing production knowledge graph used for creative intent understanding.

## Approach / System design
The work uses large language models to generate hierarchical relationships over the graph. The generation strategy is chosen by graph scale: for smaller, domain-specific graphs (under 100,000 nodes), few-shot prompting combined with one-shot generation is effective, while larger graphs benefit from cyclical generation approaches that build the hierarchy iteratively.

## Key decisions
- Use LLMs to synthesize hierarchy rather than mining it purely from existing graph structure.
- Select the prompting/generation strategy based on graph size and domain specificity instead of one universal recipe.

## Stack
Neural transformers / large language models as the core hierarchy-generation engine, applied to Adobe's production knowledge graph.

## Results
Hierarchy coverage increased by 98% for intents and 99% for colors within the knowledge graph.

## Takeaways
LLM-based generation can effectively fill in missing taxonomy in production knowledge graphs, but the right strategy depends on graph scale — few-shot plus one-shot for smaller domain graphs, cyclical generation for larger ones. Published at ECIR 2024.
