---
id: cs1870
title: Machine learning can boost the value of wind energy
company: Google DeepMind
primary_category: forecast
sub_category: capacity
year: 2019
source_url: https://deepmind.google/blog/machine-learning-can-boost-the-value-of-wind-energy/
tags: [wind-power, energy-forecasting, neural-network, grid-commitments, scheduling]
---

# Machine learning can boost the value of wind energy
**Google DeepMind** · 2019 · [source](https://deepmind.google/blog/machine-learning-can-boost-the-value-of-wind-energy/)

## Problem
Wind power is intermittent and difficult to predict, making it hard for operators to commit to day-ahead grid delivery schedules. Under-delivery versus committed output incurs financial penalties, while over-delivery is wasted capacity, so poor forecasting directly erodes the economic value of wind assets.

## Approach / System design
DeepMind deployed a neural network trained on weather forecast data and historical turbine output to predict wind farm generation 36 hours ahead. The 36-hour forecast horizon matches the day-ahead scheduling window used by electricity grid operators, allowing the system to recommend specific delivery commitments that maximise revenue while managing under-delivery risk.

## Key decisions
Aligning the forecast horizon to the grid's day-ahead commitment window was a practical design decision that directly couples model outputs to the economic value mechanism. Training the model across 700 MW of Google's US wind portfolio rather than per-farm created a shared representation of weather patterns across sites.

## Stack
Neural network forecasting model, weather forecast inputs, historical turbine output data, integrated with day-ahead grid scheduling across approximately 700 MW of US wind capacity.

## Results
The system increased the economic value of wind energy by approximately 20% compared to a baseline without ML-based scheduling.

## Takeaways
Aligning ML forecast outputs directly to grid scheduling products — rather than minimising raw forecast error — is critical for extracting economic value from wind energy prediction. Even relatively modest forecast improvements translate into substantial financial gains at large wind capacity scales.
