---
id: cs2295
title: Simulator-based Reinforcement Learning for Data Center Cooling Optimization
company: Meta
primary_category: rl
sub_category: simulation
year: 2024
source_url: https://engineering.fb.com/2024/09/10/data-center-engineering/simulator-based-reinforcement-learning-for-data-center-cooling-optimization/
tags: [simulation, energy-efficiency, data-center, cooling, physics-based-model, offline-rl]
---

# Simulator-based Reinforcement Learning for Data Center Cooling Optimization
**Meta** · 2024 · [source](https://engineering.fb.com/2024/09/10/data-center-engineering/simulator-based-reinforcement-learning-for-data-center-cooling-optimization/)

## Problem
Cooling is a major consumer of energy and water in Meta's data centers. Supply airflow setpoints are the primary lever on supply fan energy and water usage, but they must be tuned while keeping halls within strict operating bounds (65–85°F temperature, 13–80% humidity). Manual tuning is labor-intensive, and exploring setpoints on live systems risks thermal violations and service impact.

## Approach / System design
Meta trained an RL policy entirely offline inside a physics-based thermal simulator built on differential equations. Starting from historical sensor observations, the agent samples candidate airflow setpoints, the simulator predicts the resulting thermal states and an efficiency reward, and a deep neural network policy learns to map environmental conditions to optimal supply airflow setpoints. The trained policy integrates with the building management system (BMS) for deployment.

## Key decisions
- Train offline in simulation rather than on live infrastructure, eliminating deployment risk from exploration (no thermal violations or service breaches during learning).
- Use a physics-based simulator instead of a purely data-driven model, enabling training on scenarios never observed historically and transfer to newly designed facilities.
- Optimize airflow setpoints specifically — temperature/humidity bounds are fixed constraints, while airflow directly drives fan energy and water consumption.

## Stack
Physics-based thermal simulator (differential-equation model), deep neural network policy, historical sensor data for initialization, BMS integration for actuation.

## Results
- 20% reduction in supply fan energy consumption in one pilot region, averaged across weather conditions.
- 4% reduction in water usage across various weather conditions.
- Temperature conditions stayed within specification throughout the deployment.

## Takeaways
Simulator-based offline RL makes RL viable for safety-critical physical infrastructure: the simulator absorbs the risk of exploration, and physics grounding lets the same approach generalize to unseen conditions and future facilities. Meta plans to apply the methodology during the design phase of AI-optimized data centers, replacing labor-intensive manual tuning with continuous optimization.
