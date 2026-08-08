---
id: cs1867
title: GraphCast: AI model for faster and more accurate global weather forecasting
company: Google DeepMind
primary_category: forecast
sub_category: time-series
year: 2023
source_url: https://deepmind.google/blog/graphcast-ai-model-for-faster-and-more-accurate-global-weather-forecasting/
tags: [weather-forecasting, graph-neural-network, ERA5, ECMWF, deep-learning]
---

# GraphCast: AI model for faster and more accurate global weather forecasting
**Google DeepMind** · 2023 · [source](https://deepmind.google/blog/graphcast-ai-model-for-faster-and-more-accurate-global-weather-forecasting/)

## Problem
Physics-based numerical weather prediction systems require hours of supercomputer time to produce a single 10-day global forecast, limiting the frequency and timeliness of forecast updates. Existing ML-based alternatives had not consistently matched the accuracy of operational NWP at medium-range horizons.

## Approach / System design
GraphCast represents the atmosphere as a multi-scale graph over the globe and uses a graph neural network to iteratively propagate information across the mesh. The model autoregressively steps forward in 6-hour increments and was trained on 40 years of ERA5 reanalysis data from ECMWF, learning a data-driven emulator of the complex dynamics underlying atmospheric evolution.

## Key decisions
Choosing a GNN architecture over a regular grid representation allows the model to naturally handle the irregular connectivity of atmospheric teleconnections without the distortions introduced by latitude-longitude grids. Training on ERA5 reanalysis — the most comprehensive long-record atmospheric dataset — provides both the volume and quality of data needed to learn generalizable weather dynamics.

## Stack
Graph neural network (multi-scale mesh), ERA5 reanalysis training data, single TPU v4 for inference, operated as a live experiment within ECMWF's production workflow.

## Results
GraphCast produces a 10-day global weather forecast in under one minute on a single TPU. ECMWF adopted it as a live experiment in their operational forecasting system.

## Takeaways
Graph neural networks trained on large reanalysis archives can match or exceed the accuracy of physics-based NWP at a small fraction of the computational cost. The model's adoption as a live ECMWF experiment validates that data-driven approaches have crossed the threshold of operational reliability.
