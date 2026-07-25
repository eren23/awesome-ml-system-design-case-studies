---
id: cs2270
title: Evolution of Enforcing Professional Community Policies at Scale at LinkedIn
company: LinkedIn
primary_category: moderation
sub_category: policy-enforcement
year: 2024
source_url: https://www.linkedin.com/blog/engineering/trust-and-safety/evolution-enforcing-our-professional-community-policies-at-scale
tags: [policy-enforcement, llm, community-guidelines, trust-and-safety, ml-pipeline, content-review]
---

# Evolution of Enforcing Professional Community Policies at Scale at LinkedIn
**LinkedIn** · 2024 · [source](https://www.linkedin.com/blog/engineering/trust-and-safety/evolution-enforcing-our-professional-community-policies-at-scale)

## Problem
LinkedIn must enforce member restrictions — account limitations for policy violations — across 1B+ members, with the restriction check sitting in the hot path of nearly every request: 4–5 million QPS, sub-5ms latency budgets, and 99.999% availability requirements. The original architecture could not keep up as the platform decomposed into microservices.

## Approach / System design
Three generations of the enforcement system:
1. **Gen 1**: Oracle relational database with CRUD workflows over distributed tables; became a bottleneck as the platform scaled out to microservices.
2. **Gen 2**: Migration to Espresso (LinkedIn's NoSQL store) with Kafka-based event streaming; each host bootstrapped the full restriction dataset into in-memory caches (FastUtil collections), eliminating network calls per check. This saved 16TB+ of aggregate memory across 100+ client services but suffered 30+ minute bootstrap times on deployment.
3. **Gen 3**: Adoption of Venice's DaVinci client library, streaming restriction records via Kafka into off-heap storage, with bitset-like data structures to shrink the memory footprint and avoid GC latency spikes.

Restriction decisions themselves are produced upstream by ML models, rule-based systems, and human review (the CASAL platform); this system is the low-latency enforcement/distribution layer.

## Key decisions
- Prioritize consistency and availability in the CAP trade-off for enforcement data.
- Progress through caching strategies deliberately: server-side → client-side → full refresh → Bloom filters → distributed streaming.
- Move from HashMap-style structures to bitset-like structures, and from on-heap to off-heap memory, to control both footprint and GC pauses.
- Use near-real-time streaming (Kafka + Brooklin) so newly restricted accounts are enforced quickly platform-wide.

## Stack
Oracle → Espresso (NoSQL), Kafka and Brooklin for streaming, Venice DaVinci client-side caching, FastUtil collections, upstream detection via ML models, rules, and human review through CASAL.

## Results
- Sustains 4–5M QPS at <5ms latency with 99.999% availability.
- Large per-host memory-footprint reductions and elimination of long bootstrap delays.
- Faster enforcement latency for newly restricted accounts.

## Takeaways
Enforcement at hot-path scale is a data-distribution problem as much as an ML problem: each generation traded a new bottleneck (DB throughput, bootstrap time, GC pauses) for the next optimization. The team's own lessons: start simple and scale thoughtfully, identify design ceilings before they become incidents, and lean on benchmarking and cross-team infrastructure (Venice) rather than bespoke solutions.
