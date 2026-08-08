---
id: cs1882
title: ConSTGAT: Contextual Spatial-Temporal Graph Attention Network for Travel Time Estimation at Baidu Maps
company: Baidu
primary_category: forecast
sub_category: eta-prediction
year: 2020
source_url: https://dl.acm.org/doi/10.1145/3394486.3403320
tags: [travel-time-estimation, graph-attention, spatial-temporal, multi-task-learning, production-deployment]
---

# ConSTGAT: Contextual Spatial-Temporal Graph Attention Network for Travel Time Estimation at Baidu Maps
**Baidu** · 2020 · [source](https://dl.acm.org/doi/10.1145/3394486.3403320)

## Problem
Accurate travel time estimation (ETA) at map scale must capture both spatial correlations between road segments and temporal patterns such as rush-hour effects. Earlier models handled these dimensions in isolation or with limited context, resulting in systematic estimation errors at high traffic volumes.

## Approach / System design
ConSTGAT jointly models spatial and temporal correlations using a graph-attention network that operates over the road network topology. A contextual convolutional component complements the graph model by capturing broader situational context, and the two components are unified through multi-task learning so that auxiliary prediction targets reinforce the shared representation.

## Key decisions
Using multi-task learning to tie together the graph-attention and contextual convolutional branches avoids training each component independently and encourages the model to learn complementary features. Graph-attention mechanisms allow the model to assign learned importance weights to neighbouring road segments rather than treating all neighbours equally.

## Stack
Graph attention network, contextual convolutional model, multi-task learning framework, deployed within Baidu Maps production infrastructure.

## Results
The system was deployed in production at Baidu Maps, where it serves tens of billions of ETA requests daily.

## Takeaways
Jointly modelling spatial topology and temporal context within a single end-to-end trained architecture improves ETA quality at production scale. Multi-task learning is an effective mechanism for coupling complementary inductive biases without requiring separate training pipelines.
