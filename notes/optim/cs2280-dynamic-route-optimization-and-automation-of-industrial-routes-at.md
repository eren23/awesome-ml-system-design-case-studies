---
id: cs2280
title: Dynamic Route Optimization and Automation of Industrial Routes at WM
company: WM
primary_category: optim
sub_category: routing
year: 2026
source_url: https://pubsonline.informs.org/doi/10.1287/inte.2025.0279
tags: [vehicle-routing, dynamic-routing, automation, operations-research, informs]
---

# Dynamic Route Optimization and Automation of Industrial Routes at WM
**WM** · 2026 · [source](https://pubsonline.informs.org/doi/10.1287/inte.2025.0279)

## Problem
WM, North America's largest waste and recycling company, had 150+ planners manually building ~3,800 industrial (roll-off) routes daily for 22,000+ service requests across 460 hauling sites — 4–5 hours per site every day. Manual routes violated time windows over 11% of the time and exceeded maximum route limits over 28% of the time. The problem is genuinely hard: 20+ service types, 100+ container sizes, 70+ waste classifications, tandem vehicles, carry-cans, multi-facility coordination, and demand that swings with weather, season, and holidays. Two previous automation attempts had failed.

## Approach / System design
A two-stage analytical pipeline. Stage 1: demand forecasting and capacity planning, replacing trimmed moving averages with per-day-of-week ARIMA models over a 14-day horizon, handling day/night volumes and same-day requests (MAPE improved from 30–35% to 25%; Prophet reached 15% in testing). Stage 2: automated route optimization for the roll-off VRP with time windows, treated as NP-hard and solved with a multithreaded large neighborhood search metaheuristic — random ticket removal/reinsertion, intra-route moves (swaps, two-opt, group moves), inter-route redistribution, service-type alteration, and intensification cycles. Travel times come from proprietary truck-calibrated OD matrices built from millions of GPS points, respecting truck weight, dimensions, and bridge clearances.

## Key decisions
- LNS metaheuristic over exact methods for scalability at enterprise problem sizes.
- Two-phase solving: tandem-only routing first, then remaining tickets, to avoid tandem misallocation.
- Heavy stakeholder engagement — algorithm transparency and iterative refinement with the 150+ planners — explicitly to overcome skepticism from the two prior failed attempts.
- Pilot on 25 representative sites before rolling out to all 460, with a 3-year phased timeline (June 2021 to Q3 2024) and visible CEO/COO sponsorship.
- Data digitalization and a centralized enterprise data warehouse built before the algorithms.

## Stack
ARIMA (and Prophet in testing) for forecasting; large neighborhood search with multithreading for routing; proprietary truck-calibrated travel-time computation on AWS Graviton 3 servers; enterprise data warehouse with centralized data marts; commercial truck navigation systems.

## Results
Pilot (25 sites, 2023): 10.3% better hours-per-haul efficiency, 11.6% lower mileage per haul, full constraint compliance. Enterprise rollout (Q3 2024): $11M annual savings from 1.24% YoY efficiency gains, plus $1M from role reductions; 50% fewer bridge overhead strikes; 10% improvement in meeting sub-4-hour service windows; 157 bps margin expansion — the best ever for the industrial line (~14% of revenue, $3.1B in 2024). Route building dropped from 4–5 hours per site to under 45 minutes. Solver reaches within 1% of best-known solutions in under a minute for small instances and ~41 minutes for cross-site problems of 155 routes / 1,151 tickets; cross-site pooling pilots added 2–3% further efficiency. Projected future benefits: $25–42M from total cost optimization and $26–30M in truck capital avoidance.

## Takeaways
The third attempt succeeded because of change management, not just better math: executive commitment, algorithm transparency for frontline planners, and data infrastructure built first. Automating routing also seeded a lasting organizational capability — a business optimization function and a repeatable playbook now aimed at other lines of business.
