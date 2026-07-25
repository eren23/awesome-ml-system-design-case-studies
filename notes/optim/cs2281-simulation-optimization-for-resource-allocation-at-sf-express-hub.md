---
id: cs2281
title: Simulation-Optimization for Resource Allocation at SF Express Hub
company: SF Express
primary_category: optim
sub_category: allocation
year: 2024
source_url: https://pubsonline.informs.org/doi/10.1287/inte.2024.0187
tags: [simulation-optimization, resource-allocation, hub-operations, staffing, informs]
---

# Simulation-Optimization for Resource Allocation at SF Express Hub
**SF Express** · 2024 · [source](https://pubsonline.informs.org/doi/10.1287/inte.2024.0187)

## Problem
SF Express's Shenzhen parcel-sorting hub planned labor, equipment, and workstation allocation with spreadsheets. As parcel volume volatility grew and fulfillment windows tightened, this manual planning kept producing mismatches between resources and actual operational load across the hub.

## Approach / System design
The team built a two-component framework: a discrete-event simulation model that captures operational variability and the interdependencies between sorting processes, with an optimization solver embedded inside it that searches for cost-effective resource plans under real-world constraints. The tool was deliberately designed so frontline operational staff could run it without analytics expertise.

## Key decisions
- Start with high-priority ground-to-air flows, where outbound flight schedules make constraints tightest, before broadening scope.
- Run a three-phase field test (March–April 2024) to validate the simulation and then the embedded solver against practice.
- Scale the validated approach across the entire hub's operations over the rest of 2024.
- Prioritize usability by operations staff over analytical sophistication so the tool could be deployed quickly.

## Stack
Discrete-event simulation with an embedded mathematical optimization solver, integrated as a data-driven decision-support tool for hub planners.

## Results
Field tests showed an 18.7% cost reduction from simulation-driven plan refinement and up to 33.5% savings once the optimization solver was engaged. Scaled across all hub operations for the remainder of 2024, the system delivered an average 11% cost reduction, with the largest gains in air-bound flows constrained by outbound scheduling.

## Takeaways
Pairing simulation rigor with a solver, then wrapping both in a tool operational teams can actually use, converts one-off analytical wins into sustained savings. The biggest returns came where scheduling constraints were hardest, suggesting simulation-optimization pays off most in the tightest-coupled parts of a logistics operation.
