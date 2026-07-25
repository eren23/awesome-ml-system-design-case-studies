---
id: cs2116
title: Print Demand Forecasting with Machine Learning at HP Inc.
company: HP Inc.
primary_category: forecast
sub_category: demand-forecast
year: 2024
source_url: https://pubsonline.informs.org/doi/10.1287/inte.2024.0126
tags: [demand-forecast, lightgbm, supply-chain, manufacturing, human-in-the-loop, multi-sku, demand-forecasting]
---

# Print Demand Forecasting with Machine Learning at HP Inc.
**HP Inc.** · 2024 · [source](https://pubsonline.informs.org/doi/10.1287/inte.2024.0126)

## Problem
HP manufactures over 18,000 print products sold across 170 countries, with heterogeneous and dynamic demand patterns. Forecasting relied on manual consensus processes requiring expert correction plus basic time-series models with unsatisfactory accuracy. Forecast errors translated directly into inventory imbalances and delivery failures, hurting profitability.

## Approach / System design
The team built a human-in-the-loop forecasting process that combines a machine learning model with the existing consensus and statistical forecasting workflows. The ML system automates prediction across the SKU portfolio while preserving expert judgment for handling uncertainty, and is deployed inside HP's existing supply planning workflows for manufacturing, inventory, and shipment scheduling.

## Key decisions
- LightGBM as the forecasting algorithm, chosen for its ability to handle complex, heterogeneous multi-SKU demand data.
- Keep human consensus planners in the loop rather than fully automating, so experts handle the uncertainty the model cannot.
- Integrate into existing supply-chain planning processes instead of standing up a parallel system.
- Establish methodological foundations designed for ongoing algorithm evolution.

## Stack
LightGBM (gradient-boosted trees); other infrastructure details are not covered in the source.

## Results
The ML model reduced systematic errors compared with the incumbent consensus and statistical approaches and was validated sufficiently for enterprise-wide deployment. Specific quantitative improvements are not detailed in the accessible abstract.

## Takeaways
Two lessons the authors generalize beyond forecasting: build strong methodological foundations so the algorithmic core can evolve, and actively manage collaboration across distributed teams — enterprise-scale ML succeeds or fails as much on organizational execution as on model choice.
