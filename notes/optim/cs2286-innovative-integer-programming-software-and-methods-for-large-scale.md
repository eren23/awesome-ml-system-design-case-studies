---
id: cs2286
title: Innovative Integer Programming Software and Methods for Large-Scale Routing at DHL Supply Chain
company: DHL
primary_category: optim
sub_category: routing
year: 2024
source_url: https://pubsonline.informs.org/doi/10.1287/inte.2023.0087
tags: [vehicle-routing, integer-programming, large-scale, milp, informs]
---

# Innovative Integer Programming Software and Methods for Large-Scale Routing at DHL Supply Chain
**DHL** · 2024 · [source](https://pubsonline.informs.org/doi/10.1287/inte.2023.0087)

## Problem
DHL Supply Chain North America moves over one billion packages a year and needed a competitive edge in transportation planning: optimizing customer delivery routes, designing networks, sizing fleets, and backing cost-reduction guarantees in competitive bids for corporate customers.

## Approach / System design
The Transport Network Optimization (TNO) software suite, built with academic partners at Ohio State University, integrates four modules:
1. Freight optimization including make-buy (outsourcing) decisions
2. Fleet sizing optimization
3. Connection hub / pool point optimization
4. Round-trip optimization

The suite is built on integer programming, with algorithmic innovations to make large-scale instances tractable.

## Key decisions
- A multi-module architecture covering the distinct routing problems planners face (freight, fleet, hubs, round trips) rather than a single monolithic solver.
- A novel "two-color ant colony search" variant to efficiently handle the make-buy/outsourcing structure in freight optimization.
- Dynamic programming for subproblems inside the larger optimization framework.
- Industry-academia collaboration to turn research methods into deployment-ready software.

## Stack
Integer programming (MILP) core; two-color ant colony search metaheuristic; dynamic programming for subproblems. Published in INFORMS journal (Franz Edelman competition track).

## Results
Over roughly 2.5 years from 2020:
- ~$117 million in estimated cumulative savings for DHL and its customers.
- 20% increase in competitive bid win rate.
- At least 0.1 megatons of CO2 emissions reduction.

## Takeaways
Large-scale routing value came from matching specialized algorithms to problem structure — notably the ant-colony variant for outsourcing decisions — inside a modular suite planners can apply across bid, design, and operations work. Optimization tooling improved not just operating cost but commercial win rate, and delivered measurable sustainability gains as a side effect.
