---
id: cs2384
title: Lufthansa increases on-time flights by wind forecasting with Google Cloud ML
company: Lufthansa
primary_category: forecast
sub_category: time-series
year: 2022
source_url: https://cloud.google.com/blog/products/ai-machine-learning/how-lufthansa-reduce-flight-delays-with-google-cloud-ml
tags: [vertex-ai, time-series, wind-forecasting, flight-delays, weather-prediction, automl, scheduling, weather forecasting, deep learning, airline, Vertex AI, class imbalance]
---

# Lufthansa increases on-time flights by wind forecasting with Google Cloud ML
**Lufthansa** · 2022 · [source](https://cloud.google.com/blog/products/ai-machine-learning/how-lufthansa-reduce-flight-delays-with-google-cloud-ml)

## Problem
The BISE — a cold, dry northeast wind in Switzerland — can cut Zurich Airport's capacity by up to 30%, forcing delays and cancellations that cost millions in lost revenue. Predicting BISE speed and magnitude with traditional meteorological methods is very difficult, so Lufthansa (with Zurich Airport) wanted an ML forecast that network controllers could act on hours ahead.

## Approach / System design
Five years of MeteoSwiss weather simulation data at 10-minute resolution feeds the pipeline. Preprocessing and feature engineering happen in Vertex AI Workbench; Vertex AI Pipelines orchestrates the training workflow; raw data sits in Cloud Storage; Vertex AI Forecast (AutoML) trains the time-series model; results land in BigQuery for analysis. Since BISE cannot be measured directly, the team engineered "tailwind speed around the runway" as a proxy target variable.

## Key decisions
- Engineered a proxy target (runway tailwind speed) rather than trying to predict an unmeasurable phenomenon directly.
- Picked AutoML (Vertex AI Forecast) over hand-built deep learning models, trading customization for speed to production.
- Addressed severe class imbalance (BISE events are rare) with three sample-weighting schemes: inverse square root of sample count (ISNS), effective number of samples (ENS), and Gaussian reweighting.
- Used managed components end to end (Managed Datasets, Model Registry, Pipelines) to keep the workflow reproducible.

## Stack
Vertex AI Workbench, Vertex AI Pipelines, Vertex AI Forecast (AutoML), Vertex AI Managed Datasets and Model Registry, Cloud Storage, BigQuery; MeteoSwiss simulation data.

## Results
- 40% relative improvement over Lufthansa's internal heuristics for 2-hour-ahead forecasts, and roughly 1700% better than a random baseline.
- The advantage widens at longer horizons (e.g., 6 hours), which matters most for proactive runway scheduling.
- A working, production-grade model in days rather than the months a typical ML project takes.

## Takeaways
- Careful target engineering (a measurable proxy) can make an "unpredictable" phenomenon learnable.
- Class-imbalance reweighting is essential when the operationally important events are rare.
- AutoML delivered better-than-heuristic accuracy fast; next step is embedding forecasts into Lufthansa's Operations Decision Support Suite for network controllers.
