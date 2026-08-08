---
id: cs1872
title: Using AI to expand global access to reliable flood forecasts
company: Google
primary_category: forecast
sub_category: time-series
year: 2024
source_url: https://research.google/blog/using-ai-to-expand-global-access-to-reliable-flood-forecasts/
tags: [flood-forecasting, LSTM, hydrology, operational-system, Flood-Hub]
---

# Using AI to expand global access to reliable flood forecasts
**Google** · 2024 · [source](https://research.google/blog/using-ai-to-expand-global-access-to-reliable-flood-forecasts/)

## Problem
Reliable flood forecasts have historically been unavailable in many parts of the world, especially in low- and middle-income countries where hydrological monitoring infrastructure is sparse. Traditional physics-based river models require site-specific calibration that is infeasible at global scale.

## Approach / System design
Google trained a single global dual-LSTM model to predict streamflow at river gauges worldwide. One LSTM branch processes meteorological inputs such as precipitation and temperature while the other encodes static catchment characteristics, and their outputs are combined to estimate river discharge. The model was trained on data from 5,680 gauges and produces daily forecasts up to 7 days ahead.

## Key decisions
Training one model globally rather than separate regional or catchment-specific models was central to the approach, enabling the system to generalise to ungauged basins through transfer of learned hydrological patterns. The dual-LSTM architecture separates dynamic meteorological forcing from static catchment attributes, giving the model a clean inductive bias about how each type of information influences streamflow.

## Stack
Dual-LSTM architecture, global training on 5,680 stream gauges, deployed as Google Flood Hub with public alerting via Google Search and Maps.

## Results
The system operates in real time via Flood Hub, providing 7-day forecasts across 80+ countries and covering approximately 460 million people who live in flood-prone areas.

## Takeaways
A single globally trained deep learning model can surpass site-specific physics-based models in flood forecasting by leveraging large-scale cross-catchment learning. Operationalising the model through a consumer-facing product (Flood Hub) demonstrates how ML-based hydrology can have direct humanitarian impact.
