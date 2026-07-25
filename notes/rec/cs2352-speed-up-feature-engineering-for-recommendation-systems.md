---
id: cs2352
title: Speed Up Feature Engineering for Recommendation Systems
company: Snap
primary_category: rec
sub_category: personalization
year: 2024
source_url: https://eng.snap.com/speed-up-feature-engineering
tags: [feature-engineering, recommendation-systems, production, efficiency, real-time]
---

# Speed Up Feature Engineering for Recommendation Systems
**Snap** · 2024 · [source](https://eng.snap.com/speed-up-feature-engineering)

## Problem
Feature engineering was a major bottleneck for Snap's recommendation ML teams. The traditional "forward-fill" approach forced ML engineers to modify production services to start logging a new feature — a risky, coordination-heavy change with feedback loops measured in weeks. Feature infrastructure was also fragmented across teams, making features hard to share and leaving smaller teams without advanced capabilities.

## Approach / System design
Snap built Robusta, a declarative feature platform focused on associative and commutative aggregation features, which make up over 80% of the signals in their models. It uses a lambda architecture: a streaming pipeline computes minute-level pre-aggregations while a batch pipeline produces hour/day-level aggregations for completeness. Intermediate aggregation blocks are stored at multiple time granularities and assembled on demand into sliding-window features. Pre-aggregated statistics live in Apache Iceberg tables for offline use, and features are served online from Aerospike. Engineers define features in declarative YAML configs with SQL transforms and aggregation definitions — no production-service changes required.

## Key decisions
- Restrict scope to associative/commutative aggregations, whose mathematical properties enable hierarchical time-block decomposition and cheap sliding-window computation.
- Declarative YAML + SQL feature definitions so ML engineers never touch production serving code.
- Merge-on-read storage strategy, trading write efficiency for experiment velocity and frequent backfills.
- Bucketed joins with consistent partitioning to minimize shuffle during offline feature generation.
- Point-in-time correctness via version pointers so offline training data matches online serving behavior.

## Stack
Apache Spark (streaming and batch aggregation), Apache Iceberg (pre-aggregated offline storage), Aerospike (online key-value serving), Parquet (offline output format), YAML/SQL declarative feature definitions.

## Results
The source states the launch produced many impactful features and sizable business gains, without publishing specific metrics. The main measured improvement is workflow-level: new aggregation features no longer require production changes or weeks of logging lag before they can be trained on.

## Takeaways
Most recommendation features fall into a small number of aggregation patterns; automating that 80% case removes the riskiest and slowest part of feature iteration. Exploiting algebraic properties (associativity, commutativity) is what makes the storage and compute design scale, and point-in-time correctness between offline training and online serving has to be designed in, not bolted on.
