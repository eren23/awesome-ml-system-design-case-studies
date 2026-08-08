---
id: cs2425
title: Mitigating risk: AWS backbone network traffic prediction using GraphStorm
company: Amazon
primary_category: graph
sub_category: gnn
year: 2023
source_url: https://aws.amazon.com/blogs/machine-learning/mitigating-risk-aws-backbone-network-traffic-prediction-using-graphstorm/
tags: [gnn, graphstorm, network-traffic, infrastructure, aws, backbone-network, traffic-prediction, risk-mitigation]
---

# Mitigating risk: AWS backbone network traffic prediction using GraphStorm
**Amazon** · 2023 · [source](https://aws.amazon.com/blogs/machine-learning/mitigating-risk-aws-backbone-network-traffic-prediction-using-graphstorm/)

## Problem
Amazon's backbone network carries massive volumes of inter-service traffic across data centers and regions, and unexpected traffic surges can overwhelm links and create outages. Network engineers needed accurate traffic forecasts to make proactive capacity decisions and reduce the risk of congestion on critical infrastructure links.

## Approach / System design
AWS applied GraphStorm, its open-source graph machine learning framework, to build GNN-based models that represent the backbone network as a graph, with nodes corresponding to network devices and edges capturing traffic relationships. The model ingests historical traffic telemetry and the topological structure of the network to generate per-link traffic predictions, enabling capacity teams to anticipate demand rather than react to it.

## Key decisions
Framing the problem as a graph prediction task rather than a purely time-series problem allows the model to incorporate structural dependencies between network nodes, which point-to-point forecasters miss. GraphStorm's support for large-scale distributed GNN training was necessary given the size of Amazon's backbone topology.

## Stack
GraphStorm (AWS open-source GNN framework), graph neural networks, AWS infrastructure for distributed training.

## Results
Not covered in the source.

## Takeaways
Representing network topology as a graph and applying GNNs allows traffic prediction models to leverage structural context that standard time-series models ignore. GraphStorm provides a scalable path for applying graph ML to large production infrastructure graphs without building custom distributed training pipelines from scratch.
