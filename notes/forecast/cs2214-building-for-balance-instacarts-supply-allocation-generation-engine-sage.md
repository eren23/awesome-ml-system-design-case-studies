---
id: cs2214
title: "Building for Balance: Instacart's Supply Allocation & Generation Engine (SAGE)"
company: Instacart
primary_category: forecast
sub_category: demand-forecast
year: 2024
source_url: https://www.instacart.com/company/tech-innovation/building-for-balance
tags: [supply-demand-balancing, linear-programming, forecasting, marketplace, gig-economy, optimization, incentives]
---

# Building for Balance: Instacart's Supply Allocation & Generation Engine (SAGE)
**Instacart** · 2024 · [source](https://www.instacart.com/company/tech-innovation/building-for-balance)

## Problem
Instacart's marketplace requires shopper supply and customer demand to stay in equilibrium — imbalance in either direction erodes trust with both sides. The team needed to (1) forecast upcoming marketplace health and (2) decide which intervention levers to pull, at what level, to restore balance cost-effectively.

## Approach / System design
A two-stage system: a forecasting component predicts organic shopper supply and customer demand across geographies and time horizons, quantifying the incremental shoppers or customers needed when forecasts deviate from targets; a balancing engine then evaluates three lever categories — shopper onboarding, incentives to existing/churned shoppers, and customer incentivization — and allocates spend optimally. SAGE v1 (2020) was a single global linear program with heuristic inputs, constant-efficiency assumptions, a one-week horizon, and pooled geographies. V2 extended to 6-week joint optimization, replaced constant efficiencies with nonlinear efficiency curves from uplift models (discretized into a mixed-integer program), and parallelized optimization to the region level using Celery on AWS.

## Key decisions
- Extend the planning horizon from one week to six weeks of joint optimization, enabling forward-looking budget distribution across time.
- Model heterogeneous treatment effects via uplift models and handle the resulting nonlinear efficiency curves through MIP discretization (binary assignment) rather than QP solvers, to fit production latency constraints.
- Move from a single global optimization to per-region parallel runs, which also removed spillover effects that were contaminating A/B tests.
- Choose Python-MIP over PuLP and Mystic for robustness on complex MIPs.

## Stack
Python-MIP solver, uplift models for treatment-effect estimation, Celery cluster orchestration on AWS. The approach is covered by patent application 17/556,936.

## Results
V2 meaningfully reduced estimated lost customer demand caused by insufficient delivery-slot supply, lowered aggregate intervention spend, and cut a single optimization run from over an hour to substantially faster via parallelization. Operations teams saw a dramatic reduction in budgeting overhead.

## Takeaways
The team observed v1's strengths and shortcomings in production for about a year before committing to the overhaul. Discretization is a practical bridge when solvers can't handle nonlinear curves directly. Region-level parallelization pays twice — speed and clean experimentation. Remaining open challenges include real-time positioning, dynamic pricing, and tighter integration across marketplace systems.
