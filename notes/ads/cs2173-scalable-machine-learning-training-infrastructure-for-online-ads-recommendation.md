---
id: cs2173
title: Scalable Machine Learning Training Infrastructure for Online Ads Recommendation and Auction Scoring Modeling at Google
company: Google
primary_category: ads
sub_category: auction
year: 2025
source_url: https://arxiv.org/abs/2501.10546
tags: [training-infrastructure, embedding-tables, ads-recommendation, auction-scoring, large-scale, fault-tolerance]
---

# Scalable Machine Learning Training Infrastructure for Online Ads Recommendation and Auction Scoring Modeling at Google
**Google** · 2025 · [source](https://arxiv.org/abs/2501.10546)

## Problem
Google's ads recommendation and auction scoring models train on TPUs, but the accelerators alone don't guarantee efficiency. Three bottlenecks dominate: inefficient input generation pipelines feeding the trainers, expensive large embedding table operations, and wasted work when jobs are interrupted in shared datacenters.

## Approach / System design
The paper describes three families of software-level fixes across the end-to-end training pipeline:
1. **Shared input generation** — amortize the cost of producing training input across multiple models instead of regenerating per model.
2. **Embedding optimizations** — partitioning and pipelining of large embedding tables plus RPC coalescing to cut the overhead of distributed embedding lookups.
3. **Interruption resilience** — preemption notices and training-hold mechanisms so jobs in shared datacenters lose minimal work when preempted or hit errors.

## Key decisions
- Optimize software around the accelerators rather than waiting on hardware changes; TPUs handle the linear algebra, but the pipeline around them determines realized throughput.
- Coalesce RPCs for embedding operations to reduce communication overhead.
- Design for a shared-datacenter reality: preemption is expected, so the training system reacts to notices and holds state instead of restarting cold.

## Stack
Google production training infrastructure on TPUs; distributed embedding-table training with RPC-based communication.

## Results
- 116% performance (throughput) improvement across representative production models.
- 18% reduction in training costs.

## Takeaways
End-to-end training efficiency for ads models is won outside the accelerator: input pipelines, embedding-table communication patterns, and fault/preemption handling delivered a >2x combined effect. Amortizing shared work across models and engineering for interruptions are high-leverage moves in any large shared fleet.
