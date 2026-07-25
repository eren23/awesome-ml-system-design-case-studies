---
id: cs2217
title: How Nubank Models Risk for Smarter, Scalable Credit Limit Increases
company: Nubank
primary_category: fraud
sub_category: risk-scoring
year: 2025
source_url: https://building.nubank.com/how-nubank-models-risk-for-smarter-scalable-credit-limit-increases/
tags: [credit-risk, survival-analysis, transformer, foundation-model, nuformer, sequential-modeling]
---

# How Nubank Models Risk for Smarter, Scalable Credit Limit Increases
**Nubank** · 2025 · [source](https://building.nubank.com/how-nubank-models-risk-for-smarter-scalable-credit-limit-increases/)

## Problem
Across 122 million customers in Brazil, Mexico, and Colombia, Nubank must decide when and how much to raise credit limits: limits high enough to keep the product useful and customers satisfied, but low enough to contain default risk. The central quantity is probability of default — the likelihood a customer won't pay within a defined window, typically 60-180 days — under differing macroeconomic conditions per country.

## Approach / System design
Instead of binary default classification, Nubank models time-to-default with survival analysis, using survival curves that capture both whether risk materializes and how it evolves over time. The architecture is a two-step divide-and-conquer: (1) a robust risk-ranking model provides a stable baseline signal across customer populations; (2) survival-curve calibration layers precise, frequently refreshed risk curves on top of that ranking. This separation sidesteps the weaknesses of both non-parametric models (poor scalability, overfitting with many variables) and parametric ones (potentially wrong distributional assumptions). The team is also experimenting with foundational models trained on trillions of transaction records for risk ranking.

## Key decisions
- Survival analysis over binary classification, so decisions account for the temporal evolution of risk rather than a single-horizon label.
- Decouple ranking from calibration: keep the core ranking model stable while calibrating curves frequently as conditions change.
- Invest in operational rigor — reusable feature stores, CI/CD, drift and feature-stability monitoring, automated degradation alerts — so the system scales across three countries and survives product launches and external data changes.

## Stack
Survival-analysis models plus a risk-ranking model, reusable feature stores, CI/CD pipelines, automated alerting and concept-drift monitoring; experimental transformer-based foundation models over transaction histories (the manifest identifies this as nuFormer). Specific frameworks are not named in the post.

## Results
The post does not disclose specific default-rate or revenue metrics (the manifest cites a 70% risk reduction for equivalent populations). It emphasizes that the approach scales across Brazil, Mexico, and Colombia under different macro conditions.

## Takeaways
"Simple but robust, never static, always improving" is the stated philosophy: modular design keeps the risk system maintainable as markets mature, and frequent recalibration matters more than model exotica. Sequence-based foundation models over transactions are the next frontier for ranking quality.
