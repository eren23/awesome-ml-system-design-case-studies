---
id: cs2357
title: Chip Placement with Deep Reinforcement Learning
company: Google Brain
primary_category: rl
sub_category: policy-optimization
year: 2020
source_url: https://arxiv.org/abs/2004.10746
tags: [chip-design, policy-optimization, graph-neural-network, hardware-acceleration, tpu, edge-rl, production]
---

# Chip Placement with Deep Reinforcement Learning
**Google Brain** · 2020 · [source](https://arxiv.org/abs/2004.10746)

## Problem
Chip placement — arranging the blocks of a chip netlist on a canvas — is one of the most complex and time-consuming stages of chip design. It traditionally takes human experts several weeks per design, and must optimize power, performance, and area (PPA) simultaneously.

## Approach / System design
Placement is framed as a reinforcement learning problem: an agent sequentially places netlist nodes onto the chip canvas, with reward derived from placement-quality metrics. The key innovation is grounding representation learning in a supervised auxiliary task — predicting placement quality across diverse netlists and placements. The encoder trained on this reward-prediction task produces rich feature embeddings that are shared by the policy and value networks, enabling the agent to generalize to unseen chip designs and improve with experience across chips.

## Key decisions
- Learn transferable representations via a supervised placement-quality prediction task, rather than training a fresh policy per chip.
- Reuse the reward-prediction network as the shared encoder for both policy and value networks.
- Train across thousands of diverse chip floorplans so the policy generalizes to new netlists instead of overfitting one design.
- Optimize directly for PPA-linked reward rather than heuristic proxies alone.

## Stack
Not covered in the source beyond the neural architecture (shared encoder feeding policy and value networks).

## Results
The system produces placements in under 6 hours that are superhuman or comparable to expert human placements on modern accelerator netlists — versus weeks of expert effort with existing approaches. Per the catalog metadata, the method was applied to Google TPU v4 chip design.

## Takeaways
An RL agent can compress a weeks-long expert design loop into hours when it is given representations that transfer across problem instances. The enabling trick is not the RL algorithm itself but the supervised pretraining of a generalizable encoder — experience on past chips becomes an asset that improves placements on future ones.
