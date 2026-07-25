---
id: cs2287
title: Faster, Smarter, Leaner: How Flipkart Optimized Its Supply Chain to Unlock Growth
company: Flipkart
primary_category: optim
sub_category: logistics
year: 2026
source_url: https://pubsonline.informs.org/doi/full/10.1287/inte.2025.0282
tags: [supply-chain, central-planning, machine-learning, operations-research, edelman-finalist, big-billion-days, informs]
---

# Faster, Smarter, Leaner: How Flipkart Optimized Its Supply Chain to Unlock Growth
**Flipkart** · 2026 · [source](https://pubsonline.informs.org/doi/full/10.1287/inte.2025.0282)

## Problem
Flipkart serves 500M+ users with 150M+ products, 1.4M sellers, and 4M+ daily shipments across 19,000 zip codes. Before 2020, planning was quasi-manual and loosely coupled — teams pursued different objectives, limiting responsiveness. Demand is highly volatile (seasonality, supply disruptions, divergent customer preferences), and the COVID demand spikes past 10M daily deliveries exposed the legacy processes.

## Approach / System design
The Central Planning Platform (built 2021-2024) integrates ML and OR in a two-layer architecture: a forecasting layer (ML/deep learning demand prediction across product/geography/time granularities, with hierarchical forecast reconciliation and planner-input incorporation) feeding an operational efficiency layer of optimization models. Three tightly coupled pillars:
- Capacity planning: source-destination load estimation (bipartite graph optimization), FC personnel optimization, third-party carrier allocation (multi-criteria optimization), and real-time capacity orchestration via stochastic programming.
- Inventory planning: procurement, placement, and daily rebalancing (IWIT: excess/deficit identification → utility prioritization → large-scale MIP → truck capacity optimization, solved with parallel local neighborhood search and explainability reports).
- Network flow planning: routing, sortation, and scheduling.

## Key decisions
- Forecasting evolved deliberately: moving averages → ARIMA/exponential smoothing → CatBoost ensembles → LSTM Seq2Seq with skip connections and attention, with reconciliation for cross-hierarchy consistency.
- Stochastic programming plus probabilistic forecasts for peak-event orchestration (protecting priority orders), with reactive guardrails.
- Decomposition for scale: 10M+ decision-variable problems split into parallel subproblems, reaching ~3% optimality gap.
- Trust-building governance: rigorous back-testing, 2-3 month UATs (A/B tests, shadow mode), accuracy tracking, and interpretable outputs.

## Stack
CatBoost, LSTM Seq2Seq (+skip connections, attention), forecast reconciliation; MIP/large-scale optimization, stochastic programming, bipartite graph and multi-criteria optimization; parallel local neighborhood search heuristics.

## Results
- Forecast accuracy improved 10%-50% by category (e.g., electronics weighted MAPE 59.1% vs. 65.2% baseline).
- Capacity: 10% better shipment volume estimation, >10% higher personnel utilization, planning cycle cut from 10 days to 1 (50% cycle-time reduction overall), weekly instead of monthly refreshes.
- Peak events: 20% more high-priority two-day deliveries; handles Big Billion Days at 90M+ orders/week and 3M+ orders/peak hour.
- Inventory: one-day deliveries +50%, two-day +43%, seller working capital -10%, unhealthy inventory -50%, 500K+ units rebalanced daily.
- 2025 Edelman Award finalist.

## Takeaways
Tight integration of forecasting and optimization across pillars delivered more than isolated components could — forecast quality is the foundation everything downstream compounds on. Massive problems became tractable through decomposition rather than bigger solvers, and adoption depended on explainability, shadow testing, and governance as much as on model quality. The platform let planning teams absorb multifold growth without headcount increases.
