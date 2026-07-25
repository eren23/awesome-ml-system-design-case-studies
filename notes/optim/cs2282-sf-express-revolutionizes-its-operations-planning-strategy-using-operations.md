---
id: cs2282
title: SF Express Revolutionizes Its Operations Planning Strategy Using Operations Research
company: SF Express
primary_category: optim
sub_category: logistics
year: 2025
source_url: https://pubsonline.informs.org/doi/10.1287/inte.2025.0281
tags: [operations-research, network-planning, supply-chain, edelman-finalist, co2-reduction, informs]
---

# SF Express Revolutionizes Its Operations Planning Strategy Using Operations Research
**SF Express** · 2025 · [source](https://pubsonline.informs.org/doi/10.1287/inte.2025.0281)

## Problem
SF Express, China's largest integrated logistics provider, historically planned its network through decentralized, experience-driven regional teams. As parcel volumes exploded, this manual process could no longer coordinate decisions across 370+ gateway hubs and roughly 37,000 local hubs spanning air, road, and rail, while still meeting aggressive service-level agreements. The company needed to centralize planning and put it on an optimization footing.

## Approach / System design
Starting in 2018, an in-house OR group rebuilt planning as a centralized process using a sequential decomposition framework across four interlocking subproblems: (1) intercity air network planning (cargo flight schedules, fleet sizing, parcel routing over ~280 hubs), (2) intercity ground network planning (road/rail transshipment routes over 300+ hubs), (3) intracity feeder network planning (multi-shift vehicle routing between local and gateway hubs with dock constraints), and (4) intracity same-day networks for rapid urban delivery. Models are service network design and VRP variants on time-expanded networks, with commodities aggregated at 10-minute granularity to match SF's multi-shift pickup/delivery scheme. A network simulator vets proposed plans before rollout; headquarters sets strategy while regional teams make tactical adjustments through an interactive drag-and-drop planning interface.

## Key decisions
- Sequential decomposition instead of one monolithic model, exploiting problem structure at each layer.
- Time-expanded network formulations with unsplittable commodities (except air) to keep sortation operations simple, and in-tree constraints on ground networks for clean consolidation.
- Dual objectives: minimize cost while enforcing SLAs, with optional rewards for exceeding service targets.
- An organizational "facilitated mode" that embedded OR experts directly inside the network planning team to build trust.
- Post-processing solutions to local optimality even when global optimality was intractable, because it matched planner intuition and drove adoption.

## Stack
Mixed-integer programming with Gurobi; matheuristics combining territory-based decomposition (clustering), route domination and route-splitting rules for air, multiphase hierarchical heuristics for feeder routing, and hybrid IP plus multi-start iterated local search for same-day networks. SF Map APIs supply real-time travel-time matrices; dashboards track benefits and performance.

## Results
Over $1B in cumulative financial benefit since 2018, including $172M from January 2023 to September 2024; 1.018M tons of CO2-equivalent emissions avoided in 2023 alone. Service times improved for over 1 billion parcels, intracity vehicle trips fell 15%, vehicle utilization rose 7.6%, and half-day delivery expanded to 270+ Chinese cities. The system solves instances with ~1M commodities and 115M candidate flights within 1–2 hours for strategic analysis, and beat a commercial-solver baseline on the ground network by 13%. The work made SF Express a 2025 Edelman Award finalist and guided the decision to build Asia's first cargo-focused air hub.

## Takeaways
Large-scale network problems admit many structurally different near-optimal solutions, so strategic planning should compare scenarios rather than trust a single answer. Embedding OR staff inside the operational team, and letting planner experience shape heuristics and decompositions, was as important as the algorithms. The methodology has since been transplanted to SF's Southeast Asian operations and published as industry guidelines.
