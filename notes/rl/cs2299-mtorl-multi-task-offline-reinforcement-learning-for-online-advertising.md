---
id: cs2299
title: "MTORL: Multi-task Offline Reinforcement Learning for Online Advertising in Recommender Systems"
company: Alibaba
primary_category: rl
sub_category: policy-optimization
year: 2025
source_url: https://arxiv.org/abs/2506.23090
tags: [offline-rl, multi-task, advertising, budget-allocation, taobao, causal-state-encoder]
---

# MTORL: Multi-task Offline Reinforcement Learning for Online Advertising in Recommender Systems
**Alibaba** · 2025 · [source](https://arxiv.org/abs/2506.23090)

## Problem
Online advertising in recommender platforms hinges on two coupled decisions — which channel to recommend and how to allocate budget — but offline RL methods applied to this setting struggle with severe value overestimation under sparse advertising data, distributional shift between logged training data and live deployment, and a tendency to ignore budget constraints entirely.

## Approach / System design
MTORL frames advertising decisions as a Markov Decision Process tailored to advertising dynamics and learns from logged data. A causal state encoder captures dynamic user interests and temporal dependencies via conditional sequence modeling, with causal attention identifying correlations among causal states to strengthen user-sequence representations. A multi-task head then decodes channel recommendation and budget allocation jointly rather than as separate models. An automated online integration system deploys the multi-task decisions into Taobao's advertising stack.

## Key decisions
- Offline RL over online exploration, since live exploration in a production ad system is costly and risky.
- Joint multi-task decoding of channel and budget decisions instead of two decoupled optimizers.
- Causal sequence modeling of user state to combat overestimation and distributional shift in sparse data.

## Stack
Offline reinforcement learning with a causal state encoder, causal attention, and multi-task decoding, plus an automated deployment/integration mechanism for the online advertising system. Accepted to KDD 2025.

## Results
Experiments in offline and online environments showed MTORL outperforming state-of-the-art baselines. Deployed on Taobao's advertising system, it delivered a 0.08 CTR gain and 0.23% RPM improvement.

## Takeaways
Treating channel selection and budget allocation as one multi-task RL problem lets the policy respect the coupling between them, and causal sequence encoding is the practical lever for making offline RL stable on sparse advertising logs.
