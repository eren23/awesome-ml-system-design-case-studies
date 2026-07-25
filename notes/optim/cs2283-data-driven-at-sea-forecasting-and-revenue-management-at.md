---
id: cs2283
title: Data-Driven at Sea: Forecasting and Revenue Management at Molslinjen
company: Molslinjen
primary_category: optim
sub_category: pricing
year: 2025
source_url: https://pubsonline.informs.org/doi/10.1287/inte.2024.0177
tags: [dynamic-pricing, demand-forecasting, revenue-management, edelman-award, machine-learning, informs]
---

# Data-Driven at Sea: Forecasting and Revenue Management at Molslinjen
**Molslinjen** · 2025 · [source](https://pubsonline.informs.org/doi/10.1287/inte.2024.0177)

## Problem
Molslinjen, Denmark's largest catamaran ferry operator (8,675+ departures/year across nine routes, up to 1,200 passengers and 400 vehicles per ferry), ran forecasting and operations on expert heuristics alone. Vehicle deck packing is a time-pressured "life-size Tetris" with 20-30 minute turnarounds where mistakes cascade into delays and extra fuel burn; demand swings with seasonality, holidays, and weather; and pricing used arbitrary templates.

## Approach / System design
From 2019, Molslinjen and Danish AI firm Halfspace built an integrated platform with three components rolled out in sequence:
1. Packing optimization (first): visualizes the expected vehicle portfolio and recommends loading strategies (loose to extremely tight), replacing ad-hoc expert calls.
2. Forecasting engine (2020): XGBoost regression — 135 parallel models across demand segments — predicting passengers, vehicles, and vehicle-type mix at multiple lead times (month+/week/hour ahead), continuously updated until departure. Features include calendar effects, historical analogs, route specifics, and reservation data; k-fold (k=5) CV tuning, quarterly retraining with A/B tests.
3. Revenue management (2022): dynamic pricing over three fare classes (Business 925 DKK, Standard 749 DKK, LowFare 249-699 DKK) using EMSRb-MR with a price-dependent demand model combining parametric logistic functions and Bayesian neural networks; daily price optimization over a 2-week horizon.

## Key decisions
- Sequence the rollout: packing first for quick operational wins, then forecasting, then pricing built on the forecasts.
- Convert physical lane-meter capacity into ticket equivalents using actual vehicle lengths from the national registry, and sell above physical capacity using forecast cancellation/no-show rates.
- Bespoke system integrated with existing ticketing, cloud-hosted (Azure Databricks) but operationally separated.
- Validate pricing via counterfactual analysis (acknowledged limitation vs. A/B testing); validate forecasts on 90/10 train/test splits over five years of history.

## Stack
XGBoost (135 segment models), Bayesian neural networks + logistic demand curves, EMSRb-MR revenue management, Azure Databricks.

## Results
- Forecast accuracy: 1-hour-ahead MAE of ~8 vehicles and ~18 passengers (both ~6% MAPE); 1-week-ahead MAE 50%+ better than baseline.
- Operations: 3.5% fewer delayed departures, 1.5-minute average delay reduction, 6% more vehicles packed per departure, 3% fuel/emissions reduction worth 10-12M DKK (~$1.44-1.73M) annually.
- Revenue: on full departures (>90% capacity), 7-15% revenue increase; 1-2% overall; 5,000 extra tickets (6% more sales capacity) on full departures via cancellation/no-show prediction.
- Combined: 15-20M DKK ($2.6-3.2M) added annual profit; ~35M DKK cumulative since launch. Won the 2024 INFORMS Franz Edelman Award.

## Takeaways
A mid-sized operator captured airline-style revenue management value by building forecasting first and stacking pricing on top — most pricing upside concentrates in the ~15% of capacity-constrained departures. Leadership with airline RM experience and rapid staff adoption (management credits the tools with ~70% of the delay reduction) were as decisive as the models. The methodology is explicitly generic and portable to other ferry operators.
