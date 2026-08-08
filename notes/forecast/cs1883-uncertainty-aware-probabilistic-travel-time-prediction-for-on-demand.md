---
id: cs1883
title: Uncertainty-Aware Probabilistic Travel Time Prediction for On-Demand Ride-Hailing at DiDi
company: DiDi
primary_category: forecast
sub_category: eta-prediction
year: 2023
source_url: https://dl.acm.org/doi/10.1145/3580305.3599925
tags: [travel-time-estimation, probabilistic-forecasting, uncertainty, order-dispatch, production-deployment]
---

# Uncertainty-Aware Probabilistic Travel Time Prediction for On-Demand Ride-Hailing at DiDi
**DiDi** · 2023 · [source](https://dl.acm.org/doi/10.1145/3580305.3599925)

## Problem
Point-estimate travel time prediction systems systematically underestimate travel time, which leads to poor order-dispatch decisions in ride-hailing platforms. At DiDi's scale of billions of daily TTE queries, even small biases propagate into significant service quality degradation.

## Approach / System design
ProbTTE replaces a deterministic point prediction with an explicit probability distribution over travel time, allowing downstream systems to reason about best-case, worst-case, and expected arrival scenarios. By modelling the full predictive distribution rather than a single estimate, the system surfaces the inherent uncertainty in route timing and uses this signal to inform order-dispatch logic.

## Key decisions
Explicitly representing uncertainty rather than attempting to reduce it to a single number was the core design choice, enabling order-dispatch to make risk-aware decisions. The model was engineered to scale to billions of daily queries while maintaining real-time latency requirements.

## Stack
Probabilistic forecasting model (ProbTTE), integrated into DiDi's order-dispatch service, deployed in production since late 2022.

## Results
ProbTTE was deployed in production at DiDi starting in late 2022 and handles billions of TTE queries per day. It addresses the systematic underestimation issue that affected earlier point-estimate models.

## Takeaways
Switching from point predictions to full probability distributions for travel time estimation directly addresses the underestimation bias common in deterministic models. Probabilistic outputs are a natural fit for downstream decision systems like order dispatch that must trade off speed against reliability.
