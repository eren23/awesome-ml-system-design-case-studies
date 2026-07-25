---
id: cs2208
title: Enhancing Uber's Guidance Heatmap with Deep Probabilistic Models
company: Uber
primary_category: forecast
sub_category: demand-forecast
year: 2025
source_url: https://www.uber.com/us/en/blog/enhancing-ubers-guidance-heatmap-with-deep-probabilistic-models/
tags: [deep-learning, probabilistic-forecasting, demand-forecasting, gaussian-mixture-models, driver-earnings, heatmap, real-time]
---

# Enhancing Uber's Guidance Heatmap with Deep Probabilistic Models
**Uber** · 2025 · [source](https://www.uber.com/us/en/blog/enhancing-ubers-guidance-heatmap-with-deep-probabilistic-models/)

## Problem
New Uber drivers often need weeks of trial and error to learn the earning nuances of their market, which fuels frustration and churn. Uber wanted a heatmap giving drivers actionable, location-based guidance on where and when to drive, which requires forecasting earnings per hour (EpH) — a quantity with heavy inherent randomness from time-to-first-request, demand fluctuations, and trip length/value.

## Approach / System design
The model evolved in three phases: (1) an XGBoost baseline regressing mean EpH with MSE loss on geohashes, historical EpH, surge, and wait times; (2) a deep neural network with Gaussian negative log-likelihood loss outputting mean and variance — capturing uncertainty but oversimplifying the distribution; (3) the final system, a DNN with embedding layers predicting 3-mode Gaussian Mixture Models per hex, whose output heads produce weights, means, and standard deviations per component. It consumes over 60 contextual, near-real-time, and historical features (demand, surge multipliers, earnings history), forecasts at H3 hex-9 resolution, and refreshes the heatmap every 10 minutes. Spatial and temporal smoothing post-processes predictions to remove "islands" and "donuts," and variance is used as a filter so unreliable high-variance areas aren't highlighted.

## Key decisions
- Predict EpH rather than total earnings, to reflect real-time demand fluctuation, surge, and seasonality at fine hex granularity.
- Train on individual driver earnings instead of group-level aggregates, avoiding information loss from averaging.
- Refine spatio-temporal attribution of earnings so high-earning/short-wait areas are distinguishable from low-earning/long-wait ones.
- Correct a truncation bug: distributions truncated at zero weren't handled properly when computing mixture means, causing systematic underprediction.
- Model the full distribution (GMM) rather than point estimates, since observed earnings are multi-modal.

## Stack
Deep neural networks with embedding layers and GMM negative log-likelihood loss; XGBoost for the earlier baseline; Uber's H3 hexagonal grid (hex-9); 60+ feature real-time pipeline with 10-minute refresh. Specific training frameworks are not named.

## Results
The post reports that predictions increased average earnings per hour for exposed users and produced measurable gains in completed trip hours, without disclosing concrete percentages. Variance-based filtering prevents misleading signals by suppressing high-variance areas.

## Takeaways
Full probability distributions beat point estimates for guidance decisions. Much of the value came from data work — individual-level labels, attribution, holiday feature engineering — rather than architecture. Subtle math errors (truncation handling) can silently bias production systems. Planned next steps: real-time offer counts, variance surfaced in the UI, delivery-courier expansion, longer horizons, and personalization based on driver location and travel time.
