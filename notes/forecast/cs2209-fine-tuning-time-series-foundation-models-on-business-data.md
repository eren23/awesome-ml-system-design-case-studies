---
id: cs2209
title: Fine-Tuning Time-Series Foundation Models on Business Data
company: Salesforce
primary_category: forecast
sub_category: capacity
year: 2026
source_url: https://www.salesforce.com/blog/time-series-models-business-data/
tags: [foundation-models, moirai, fine-tuning, time-series, cloudops, telemetry, capacity-planning]
---

# Fine-Tuning Time-Series Foundation Models on Business Data
**Salesforce** · 2026 · [source](https://www.salesforce.com/blog/time-series-models-business-data/)

## Problem
Salesforce's infrastructure teams forecast capacity across hundreds of thousands of customers and dozens of global regions. The Moirai time-series foundation model offered broad zero-shot capability, but generic pretraining missed domain-specific CloudOps patterns — release cycles, holiday effects, regional growth curves — that operational-grade forecasting for infrastructure planning and cost control depends on.

## Approach / System design
The Infra Data Science team partnered with Salesforce AI Research to fine-tune Moirai on internal telemetry. They curated a CloudOps training dataset spanning compute, storage, customer behavior, spending trends, and regional patterns — 80+ metrics across 2M+ entities with 1.3B+ time steps. Holdout segments simulating future migrations and new services tested real-world generalization. The fine-tuned model was benchmarked against classical statistical baselines and existing forecasting implementations across short-, medium-, and long-term horizons using MASE, MAPE, MSIS, and CRPS, then integrated into Salesforce's configuration-driven forecasting platform with YAML-based onboarding.

## Key decisions
- Fine-tune a time-series foundation model on internal business data rather than relying on zero-shot performance or building bespoke per-service models.
- Design holdout sets around genuinely unseen situations (migrations, new services) instead of random splits, to measure generalization the way production would experience it.
- Evaluate on both point-accuracy and probabilistic/calibration metrics (MSIS, CRPS), since interval quality matters for capacity decisions.
- Ship through a config-driven platform so thousands of series can be onboarded declaratively.

## Stack
Moirai time-series foundation model (1.0 baseline, fine-tuned 1.1 Base and Large variants), Salesforce's internal forecasting platform with YAML-based series onboarding, CloudOps telemetry data.

## Results
Fine-tuned Moirai 1.1 Large versus baseline: MASE 0.853 → 0.731 (−14.3%), MAPE 0.864 → 0.725 (−16.1%), MSIS 0.541 → 0.419 (−22.6%), CRPS 0.336 → 0.291 (−13.4%), with similar gains for the Base variant. The post notes even a 0.5% accuracy improvement can translate into millions of dollars of operational impact at their scale.

## Takeaways
Foundation models are strong starting points but need fine-tuning on proprietary operational data to reach enterprise-grade accuracy — and that data is itself a competitive moat. Improvements showed up in calibration and stability, not just point error. Future directions include multi-modal forecasting that incorporates logs and deployment metadata, plus explainability tooling for forecast transparency.
