---
id: cs1874
title: ECMWF's AI forecasts become operational (AIFS)
company: ECMWF
primary_category: forecast
sub_category: time-series
year: 2025
source_url: https://www.ecmwf.int/en/about/media-centre/news/2025/ecmwfs-ai-forecasts-become-operational
tags: [weather-forecasting, graph-neural-network, transformer, operational-NWP, AIFS]
---

# ECMWF's AI forecasts become operational (AIFS)
**ECMWF** · 2025 · [source](https://www.ecmwf.int/en/about/media-centre/news/2025/ecmwfs-ai-forecasts-become-operational)

## Problem
Physics-based numerical weather prediction systems like ECMWF's IFS require enormous compute resources, limiting the frequency and resolution at which operational forecasts can be run. ECMWF needed to determine whether a machine-learned alternative could match or exceed IFS accuracy at a fraction of the energy cost.

## Approach / System design
The Artificial Intelligence Forecasting System (AIFS) uses a graph neural network encoder and decoder combined with a sliding-window transformer to produce medium-range weather forecasts. It was transitioned into operational status in February 2025, running in parallel with the physics-based IFS so forecasters have access to both systems simultaneously.

## Key decisions
Running AIFS alongside the existing IFS rather than replacing it allowed ECMWF to build operational confidence in the AI system before relying on it exclusively. The choice of a GNN encoder/decoder with a transformer backbone follows the pattern established by earlier AI weather models while benefiting from ECMWF's high-quality ERA5 training data.

## Stack
Graph neural network (encoder/decoder), sliding-window transformer, integrated into ECMWF's operational forecasting workflow alongside the physics-based IFS.

## Results
AIFS achieves approximately 1000x reduction in forecast energy consumption compared to the IFS, and shows up to 20% improvement in tropical cyclone track forecasts.

## Takeaways
AI-based weather models can reach operational quality while delivering order-of-magnitude energy savings over physics-based systems. Running AI and physics models in parallel is a pragmatic transition strategy that manages operational risk during the adoption period.
