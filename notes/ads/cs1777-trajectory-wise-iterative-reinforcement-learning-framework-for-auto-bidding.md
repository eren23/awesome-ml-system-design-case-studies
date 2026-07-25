---
id: cs1777
title: Trajectory-wise Iterative Reinforcement Learning Framework for Auto-bidding
company: Alibaba
primary_category: ads
sub_category: bidding
year: 2024
source_url: https://arxiv.org/abs/2402.15102
tags: [auto-bidding, offline-rl, exploration, safety, safe-exploration, display-advertising, iterative-training]
---

# Trajectory-wise Iterative Reinforcement Learning Framework for Auto-bidding
**Alibaba** · 2024 · [source](https://arxiv.org/abs/2402.15102)

## Problem
Auto-bidding policies are usually trained with RL in simulation, but simulated environments diverge from the real ad platform, so policies underperform once deployed. Training directly online is ruled out by safety concerns — a bad exploratory policy spends real advertiser money. The practical alternative is iterative offline RL: deploy agents, collect real interaction data, retrain offline, redeploy. The bottleneck the paper identifies is that the inherent conservatism of offline RL algorithms causes ineffective exploration and exploitation across these iterations.

## Approach / System design
The framework loops between deployment and offline training: multiple agents run in parallel on the live platform to gather interaction data, a new policy is trained offline on the collected dataset, and the improved policy is redeployed for the next round of collection. Two components attack the conservatism bottleneck. Trajectory-wise Exploration and Exploitation (TEE) rethinks both data collection and data utilization at the level of whole trajectories rather than individual steps. Safe Exploration by Adaptive Action Selection (SEAS) guards the online side, adaptively constraining actions so exploration stays safe while still producing a dataset useful for TEE.

## Key decisions
- Accept the sim-to-real gap and structure training as an iterative offline-RL loop on real platform data instead of relying on a simulator.
- Diagnose offline-RL conservatism as the performance bottleneck of the loop and address exploration/exploitation at the trajectory level (TEE).
- Pair exploration with an adaptive safety mechanism (SEAS) so online data collection cannot damage advertiser outcomes while preserving dataset quality.

## Stack
Offline reinforcement learning with parallel agent deployment on Alibaba's display advertising platform. Specific model architectures and infrastructure are not covered in the source.

## Results
The approach was validated through offline experiments and real-world experiments on Alibaba's display advertising platform; the abstract does not report specific metric numbers. The work was accepted as an oral presentation at The Web Conference 2024 (WWW'24).

## Takeaways
When online RL is unsafe and simulators are unfaithful, an iterative offline-RL loop can work — but only if the conservatism of offline algorithms is explicitly counteracted. Treating exploration and exploitation trajectory-wise, and coupling exploration with an adaptive safety gate, turns the deploy-collect-retrain cycle into genuine policy improvement on a live ad platform.
