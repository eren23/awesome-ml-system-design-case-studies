---
id: cs1868
title: GenCast predicts weather and the risks of extreme conditions with state-of-the-art accuracy
company: Google DeepMind
primary_category: forecast
sub_category: time-series
year: 2024
source_url: https://deepmind.google/blog/gencast-predicts-weather-and-the-risks-of-extreme-conditions-with-sota-accuracy/
tags: [weather-forecasting, diffusion-model, ensemble, probabilistic-forecasting, extreme-events]
---

# GenCast predicts weather and the risks of extreme conditions with state-of-the-art accuracy
**Google DeepMind** · 2024 · [source](https://deepmind.google/blog/gencast-predicts-weather-and-the-risks-of-extreme-conditions-with-sota-accuracy/)

## Problem
Deterministic weather models produce a single forecast trajectory, making it impossible to estimate the probability of extreme events or communicate forecast uncertainty to end users. Operational ensemble systems like ECMWF's ENS are accurate but computationally expensive and slow to generate large member sets.

## Approach / System design
GenCast adapts score-based diffusion model methodology to the sphere of the Earth, enabling it to learn and sample from the joint distribution of global atmospheric states. It generates a full 50+ member ensemble of 15-day forecasts by running multiple stochastic samples from the diffusion model, each representing a physically plausible future trajectory consistent with the initial state.

## Key decisions
Adapting diffusion models to the non-Euclidean geometry of the Earth's surface was a key technical challenge addressed in the design. Generating large ensembles rather than a single deterministic forecast was the central motivation, enabling risk quantification for extreme events such as hurricanes and heat waves.

## Stack
Score-based diffusion model adapted to spherical geometry, ensemble generation via stochastic sampling, trained on ERA5 reanalysis data.

## Results
GenCast produces a 50+ member ensemble for a 15-day global forecast in approximately 8 minutes. It outperforms ECMWF's operational ENS ensemble on 97% of tested forecast targets.

## Takeaways
Diffusion models are well-suited to probabilistic weather ensemble generation because they naturally represent multi-modal distributions over future atmospheric states. The speed advantage — large ensembles in minutes — makes probabilistic extreme-event risk assessment practical at operational scale.
