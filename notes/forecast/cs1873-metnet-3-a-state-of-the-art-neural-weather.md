---
id: cs1873
title: MetNet-3: A state-of-the-art neural weather model available in Google products
company: Google
primary_category: forecast
sub_category: time-series
year: 2023
source_url: https://research.google/blog/metnet-3-a-state-of-the-art-neural-weather-model-available-in-google-products/
tags: [weather-forecasting, nowcasting, neural-network, densification, lead-time-conditioning]
---

# MetNet-3: A state-of-the-art neural weather model available in Google products
**Google** · 2023 · [source](https://research.google/blog/metnet-3-a-state-of-the-art-neural-weather-model-available-in-google-products/)

## Problem
Traditional numerical weather prediction relies on pre-processed model analyses as inputs, which introduces latency and loses information from raw observations. There was also a need for high-resolution, localised forecasts at horizons beyond the few hours covered by nowcasting systems.

## Approach / System design
MetNet-3 learns directly from sparse raw observations — including surface weather stations, radar, and satellite data — using a densification technique that maps sparse point observations to a dense spatial grid that the neural network can process efficiently. Lead-time conditioning allows the single model to produce forecasts at arbitrary target lead times up to 24 hours without training separate models per horizon.

## Key decisions
Learning from raw sparse observations rather than post-processed NWP analyses was a key architectural choice that avoids introducing systematic biases from the analysis step. Lead-time conditioning as a continuous input variable rather than discrete output heads enables flexible inference and efficient use of training data across all horizons.

## Stack
Neural network with densification layer for sparse observations, lead-time conditioning, served operationally across Google weather products (Google Search, Google Maps, etc.).

## Results
MetNet-3 produces high-resolution 24-hour forecasts and is served operationally within Google's consumer weather products. It represents an advance over prior MetNet versions in both forecast horizon and accuracy.

## Takeaways
Learning directly from raw sparse observational data with a densification layer is an effective alternative to relying on NWP analyses, and it simplifies the data pipeline while preserving fine-grained information. Lead-time conditioning is a scalable technique for building a single model that serves forecasts across a wide range of horizons.
