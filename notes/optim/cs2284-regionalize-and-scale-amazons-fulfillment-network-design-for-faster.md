---
id: cs2284
title: Regionalize and Scale: Amazon's Fulfillment Network Design for Faster and Cheaper Delivery
company: Amazon
primary_category: optim
sub_category: logistics
year: 2025
source_url: https://pubsonline.informs.org/doi/10.1287/inte.2025.0295
tags: [network-design, fulfillment, regionalization, cost-optimization, edelman-finalist, informs]
---

# Regionalize and Scale: Amazon's Fulfillment Network Design for Faster and Cheaper Delivery
**Amazon** · 2025 · [source](https://pubsonline.informs.org/doi/10.1287/inte.2025.0295)

## Problem
By 2021 Amazon's US fulfillment network — hundreds of fulfillment centers shipping over a billion items a year — ran on a greedy order-assignment policy that routed each shipment to the momentarily cheapest FC regardless of capacity. This caused backlogs, high variability in which FCs served a destination, inflated transportation costs, and slower delivery. A stylized queuing model showed the core flaw: greedy assignment overloads an FC into persistent backlog, while balanced demand-capacity matching eliminates it (a ~40% service-time improvement in the toy model).

## Approach / System design
Regionalization: partition the US into 8 largely self-sufficient regions and redesign fulfillment around them.
- Regions built by clustering five-digit zip codes with k-means and integer programming, refined manually — small enough for speed, large enough for inventory diversity.
- FC Regionizer (FCR), a mixed-integer model, assigns FCs to regions, balancing capacity-demand ratios and transport cost, producing Pareto-surface options for stakeholder alignment.
- Network redesign: sortation centers specialized into origin/destination/hybrid hubs and last-mile sort centers; in-region paths simplified (direct FC-to-delivery-station where possible); cross-region flows forced through hubs for consolidation.
- Inventory: SKUs segmented into 10 velocity deciles — high-velocity items stocked regionally, slow movers nationally, with service-level monotonicity across bands.
- Supporting tools: the ITTO suite (shipment generation, middle-mile topology optimization, time-expanded network timing), the ODLB simulator to validate achievable in-region assignment via out-of-region cost penalties, the SPST speed simulator, and an extended goal-programming Order Assignment Model (OAM) allowing up to 100% artificial-cost relaxation to favor in-region fulfillment.

## Key decisions
- 8 regions as the sweet spot between delivery speed (smaller regions) and inventory breadth (larger regions).
- Regional service levels for fast SKUs, national for the tail — speed and cost gains without net inventory increase.
- Route all cross-region flow through hub infrastructure to protect truck consolidation as in-region share rose.
- Let OAM accept up to 100% shipment-level artificial cost increases, reasoning those costs didn't reflect true network value.
- Piloted in the Northeast/Mid-Atlantic in January 2023; results in ~3 weeks justified accelerating national rollout to March 2023, a month early, executed across dozens of teams in ~2 months.

## Stack
Mixed-integer programming and k-means (region design, FCR), ML + math programming for origin-destination flow generation (ITTO), time-expanded graph optimization, goal programming (OAM), and simulation tools (ODLB, SPST).

## Results
- Simulation (20% capacity surplus): 1.17x speed, 1.18x OD consolidation, 5% shorter average distance.
- Post-rollout 2023: in-region fulfillment up from 62% to 76%; distance traveled down 15%; middle-mile touchpoints down 12%; 16 million miles avoided; 600 million more Q4 units from in-region FCs vs. Q4 2022.
- US cost-to-serve down $0.45/unit year-over-year — first cost-per-unit reduction since 2018.
- 7+ billion same/next-day units globally in 2023, 9+ billion in 2024. 2025 Edelman Award finalist.

## Takeaways
Deliberately restricting flexibility — regional boundaries instead of global greedy assignment — made the network more optimizable, auditable, and fast, and unlocked secondary wins in inventory placement and inbound flows. Capacity-demand balancing principles from simple queuing models scale to a continent-sized network when embedded in structure. Winning stakeholder conviction required simulation and scenario analysis, and the payoff required simultaneous change across software, physical infrastructure, and operations over ~1.5 years.
