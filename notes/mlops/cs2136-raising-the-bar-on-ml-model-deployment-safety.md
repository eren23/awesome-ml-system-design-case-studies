---
id: cs2136
title: Raising the Bar on ML Model Deployment Safety
company: Uber
primary_category: mlops
sub_category: platform
year: 2025
source_url: https://www.uber.com/us/en/blog/raising-the-bar-on-ml-model-deployment-safety/
tags: [deployment-safety, shadow-testing, canary, backtesting, model-rollout, risk]
---

# Raising the Bar on ML Model Deployment Safety
**Uber** · 2025 · [source](https://www.uber.com/us/en/blog/raising-the-bar-on-ml-model-deployment-safety/)

## Problem
Uber's Michelangelo platform powers 400+ active use cases, ~20,000 training jobs monthly, and 15 million real-time predictions per second at peak. Probabilistic models tightly coupled to data can't be validated by static testing alone — models that look good offline fail in production via data drift and integration edge cases, and at Uber scale even small regressions cause widespread impact within minutes.

## Approach / System design
A safety framework spanning the ML lifecycle. Data/features: explicit missing-value handling with consistent null representation, identical imputation logic in training and serving, automated schema validation for type mismatches and distribution shifts. Training: offline distributional statistics (percentiles, averages, null rates), latency-budget evaluation, standardized model reports. Pre-production: backtesting on historical data plus shadow testing, where candidates run in parallel with production on identical live inputs. Rollout: gradual traffic ramp with continuous monitoring and automated rollback on breached error/latency/resource thresholds. Production: the Hue observability stack tracks operational metrics, prediction-level indicators, feature health, and statistical drift detection in real time.

## Key decisions
- Hybrid governance: platform-enforced default safeguards for every deployment, plus decentralized team-owned validation supported by tooling.
- Two shadow modes: endpoint shadowing (flexible, custom validation logic) and deployment shadow (fully automated, on by default).
- A transparent readiness score from four coverage metrics — offline evaluation, shadow deployment, unit tests, performance monitoring — complementing existing Model Excellence Scores, integrated into CI/CD.
- Always-on foundational safeguards: real-time data-quality checks, alerting, and gradual rollout with automatic rollback for all models.

## Stack
Michelangelo ML platform (since 2016); Hue observability built on Apache Flink and Apache Pinot (via Flink-as-a-Service); CI/CD integration for automated safety scoring.

## Results
By mid-2025, over 75% of critical models were onboarded to the Intermediate safety level and shadow testing covered over 75% of critical online use cases, targeting 100% in H2 2025. Regressions that previously lingered for days now surface within hours.

## Takeaways
Embedding safety into platform workflows — not process documents — is what drives adoption without slowing delivery, and transparent scoring shifts culture toward proactive safety. Future work targets generative-AI-assisted code artifacts, semantic drift detection for embedding-heavy systems, and hallucination/bias safeguards for larger models.
