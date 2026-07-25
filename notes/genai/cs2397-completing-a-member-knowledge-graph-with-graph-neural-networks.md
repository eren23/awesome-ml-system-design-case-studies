---
id: cs2397
title: Completing a Member Knowledge Graph with Graph Neural Networks
company: LinkedIn
primary_category: genai
sub_category: rag
year: 2021
source_url: https://engineering.linkedin.com/blog/2021/completing-a-member-knowledge-graph-with-graph-neural-networks
tags: [gnn, knowledge-graph, graph, link-prediction]
---

# Completing a Member Knowledge Graph with Graph Neural Networks
**LinkedIn** · 2021 · [source](https://engineering.linkedin.com/blog/2021/completing-a-member-knowledge-graph-with-graph-neural-networks)

## Problem
LinkedIn member profiles form an incomplete knowledge graph: entities such as skills, companies, and titles that genuinely apply to a member are often missing because they aren't explicitly stated in profile text. Inferring the missing entities requires reasoning over the interactions among all of a member's existing entities, not treating each entity in isolation.

## Approach / System design
The task is framed as link prediction on a bipartite member–entity graph: solid edges are known member–entity relationships, dotted edges are candidates to infer. The model, **Entity-BERT**, is a graph neural network that replaces standard neighbor aggregation with a multi-layer bidirectional transformer: attention layers (6–24 deep) compute pairwise interactions between all of a member's entities before predicting missing links — bringing BERT-style contextual aggregation from NLP into the graph setting.

## Key decisions
- Self-supervised training: mask 10% of entities per profile (grouped by entity type — skill, company, title, etc.) and train the model to recover them, avoiding the need for labeled data.
- Type embeddings: each entity category gets a type ID embedding to give the model schema context.
- Transformer aggregation instead of the averaging/weighted-averaging used by standard GNNs, which cannot capture complex multi-entity interactions.

## Stack
Graph neural network framework with a transformer (BERT-inspired) aggregation architecture. Specific infrastructure details are not covered in the source.

## Results
- **Skills recommender**: members accepted more Entity-BERT suggestions than with previous methods, and overall engagement (session metrics) improved.
- **Ads audience expansion**: an A/B test showed a statistically significant lift in Ads revenue with no degradation in click-through rates.

## Takeaways
- Averaging-style GNN aggregation is the limiting factor when entity interactions matter; transformer attention over a member's entity set captures the structure that matters.
- Self-supervised masking over profile entities scales training without manual labels.
- One graph-completion model fed measurable wins across multiple products — profile recommendations and ads targeting.
