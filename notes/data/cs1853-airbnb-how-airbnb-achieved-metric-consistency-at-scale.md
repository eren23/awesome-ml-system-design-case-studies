---
id: cs1853
title: Airbnb — How Airbnb Achieved Metric Consistency at Scale
company: Airbnb
primary_category: data
sub_category: data-quality
year: 2021
source_url: https://medium.com/airbnb-engineering/how-airbnb-achieved-metric-consistency-at-scale-f23cc53dea70
tags: [metrics, minerva, semantic-layer, single-source-of-truth, consistency]
---

# Airbnb — How Airbnb Achieved Metric Consistency at Scale
**Airbnb** · 2021 · [source](https://medium.com/airbnb-engineering/how-airbnb-achieved-metric-consistency-at-scale-f23cc53dea70)

## Problem
Different teams at Airbnb independently defined the same business metrics — such as "bookings" or "active hosts" — using slightly different logic, leading to conflicting numbers in dashboards, A/B test reports, and executive presentations. Reconciling these discrepancies consumed analyst time and eroded trust in data-driven decisions.

## Approach / System design
Airbnb built Minerva, a centralized metric platform that acts as a single source of truth for business metrics. Each metric is defined once in Minerva using a canonical specification, and that definition is then consumed consistently across analytics dashboards, experimentation platforms, and reporting tools. Minerva manages the full metric lifecycle: creation, versioning, deprecation, and downstream impact analysis when a definition changes.

## Key decisions
Treating metrics as first-class, governed artifacts rather than ad-hoc SQL snippets was the foundational shift. Centralizing definitions in a platform rather than documentation means the definition is always executable and always current. Integrating Minerva with experimentation and reporting surfaces ensures that all consumers draw from the same definition without requiring manual coordination.

## Stack
Minerva metric platform, integrated with internal analytics dashboards, A/B testing infrastructure, and reporting tools.

## Results
Not covered in the source.

## Takeaways
Metric inconsistency is fundamentally a governance problem, not just a technical one; a platform that enforces a single definition at the point of consumption is more reliable than documentation or conventions alone. Managing the full metric lifecycle — including the impact of definition changes on downstream consumers — is essential for keeping a metric catalog trustworthy as the organization evolves.
