---
id: cs1778
title: New AI advancements drive Meta's ads system performance and efficiency (Meta Lattice)
company: Meta
primary_category: ads
sub_category: ctr-prediction
year: 2023
source_url: https://ai.meta.com/blog/ai-ads-performance-efficiency-meta-lattice/
tags: [unified-model, multi-domain, delayed-feedback, pareto-feature-selection]
---

# New AI advancements drive Meta's ads system performance and efficiency (Meta Lattice)
**Meta** · 2023 · [source](https://ai.meta.com/blog/ai-ads-performance-efficiency-meta-lattice/)

## Problem
Meta's ads stack had grown into hundreds of independently optimized deep neural network models totaling trillions of parameters — one per goal/surface combination. The fragmentation slowed adoption of new AI techniques (each advance had to be re-integrated per model), wasted compute, and made the system brittle against privacy-driven reductions in data granularity.

## Approach / System design
Lattice replaces the model zoo with a single unified architecture trained via multi-domain, multi-task learning. One model learns jointly across surfaces (Instagram Feed, Stories, Reels) and across objectives, balancing advertiser and user value. Architecturally it is a Deep and Hierarchical Ensemble Network on a Transformers backbone chosen for GPU scalability, with sparse activation so the large model stays efficient per task. Temporal multi-distribution modeling handles conversion feedback delays that span seconds to days. Pareto optimization balances thousands of domains against tens of objectives without per-pair manual tuning. Resource sharing works on two levels: horizontally across domains and objectives, and hierarchically from a large upstream model down to lightweight downstream models.

## Key decisions
- Consolidate hundreds of siloed models into one multi-domain, multi-task model rather than continuing per-goal optimization.
- Use sparse activation and hierarchical distillation-style sharing so a trillion-parameter-class model remains servable.
- Model delayed feedback explicitly with temporal multi-distribution modeling instead of a single conversion distribution.
- Automate objective balancing with Pareto optimization across thousands of domains and tens of objectives.

## Stack
Deep and Hierarchical Ensemble Network on a Transformers backbone with sparse activation; trained on hundreds of billions of examples from thousands of data domains; GPU-based training and serving with two-level resource sharing.

## Results
Rolled out on Instagram, replacing hundreds of individually trained models, Lattice drove roughly an 8% improvement in ads quality through joint optimization of user and advertiser value, while reducing computational requirements via consolidation. Cross-surface knowledge sharing also improved advertiser performance and cold-start generalization.

## Takeaways
Consolidation itself was the innovation: a single model that shares knowledge across surfaces and objectives beat hundreds of specialists while costing less to run and adapting faster to new techniques and privacy constraints. The enabling pieces — sparse activation, temporal multi-distribution modeling, Pareto balancing — are what make "one big model" viable at ads scale.
