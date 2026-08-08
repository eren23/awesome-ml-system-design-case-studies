---
id: cs1832
title: How the Zoox Robotaxi Predicts Everything, Everywhere, All at Once
company: Zoox
primary_category: cv
sub_category: vlm
year: 2022
source_url: https://www.amazon.science/latest-news/how-the-zoox-robotaxi-predicts-everything-everywhere-all-at-once
tags: [autonomous-driving, perception, prediction, sensor-fusion, graph-neural-networks]
---

# How the Zoox Robotaxi Predicts Everything, Everywhere, All at Once
**Zoox** · 2022 · [source](https://www.amazon.science/latest-news/how-the-zoox-robotaxi-predicts-everything-everywhere-all-at-once)

## Problem
Safe autonomous driving requires not only detecting agents (vehicles, pedestrians, cyclists) around the vehicle but also predicting how each agent will move several seconds into the future. Predicting agents independently ignores the interactions between them — for example, whether one car will yield to another — leading to unrealistic trajectory forecasts and potentially unsafe planning decisions.

## Approach / System design
Zoox builds a 60-channel semantic image representation from its 360-degree multi-modal sensor suite (cameras, LiDAR, radar) and processes it with CNNs to produce per-agent features. A graph neural network then models interactions between agents, with edges representing the influence one agent exerts on another's predicted motion. The resulting joint model outputs trajectory distributions for all agents 8 seconds into the future and is recomputed every 100 milliseconds.

## Key decisions
Representing sensor data as a multi-channel semantic image rather than raw point clouds allows standard CNN backbones to be applied. The graph neural network layer was added specifically to capture agent-agent interactions, which CNN features alone cannot model. Running at 100 ms update intervals was a design choice balancing prediction freshness against computational cost.

## Stack
CNN backbone, graph neural networks (GNN), 360-degree multi-modal sensor fusion (cameras, LiDAR, radar), 60-channel semantic image representation.

## Results
Not covered in the source.

## Takeaways
Jointly modeling agent interactions via a graph neural network on top of CNN-extracted features substantially improves trajectory prediction realism compared to treating each agent independently. The combination of semantic image preprocessing and GNN interaction modeling is a broadly applicable pattern for multi-agent prediction in complex environments.
