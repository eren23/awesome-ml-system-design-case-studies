---
id: cs2207
title: "Data Mesh at Grab Part I: Building Trust Through Certification"
company: Grab
primary_category: data
sub_category: data-quality
year: 2025
source_url: https://engineering.grab.com/signals-market-place
tags: [data-mesh, signals-marketplace, data-certification, data-quality, data-governance, metadata, data-ownership, Hubble, data-contracts]
---

# Data Mesh at Grab Part I: Building Trust Through Certification
**Grab** · 2025 · [source](https://engineering.grab.com/signals-market-place)

## Problem
Grab's data ecosystem — spanning ride-hailing, food delivery, and financial services — hit six scaling walls: high volume and variety of data; ownership gaps causing quality issues and duplicate pipelines; a centralized data engineering team that bottlenecked distributed demand; producers unaware of downstream dependencies, so upstream changes broke pipelines; no unified source of truth despite a central warehouse; and uneven data expertise across teams.

## Approach / System design
Grab adopted a data mesh: data treated as a product, owned and served by domain teams closest to it. The cornerstone is the Signals Marketplace, a certification system built on three enablers. First, an ownership structure: teams are identified as Data Domains with appointed Business Data Owners and Technical Data Owners accountable for documentation and SLOs. Second, data contracts: formal producer-consumer agreements covering schema, SLA guarantees (freshness, completeness, retention), change-notice periods, and communication channels. Third, automated accountability: failed quality tests automatically open Data Production Incidents assigned to the Technical Data Owner for root-cause investigation. Usage dashboards in Grab's Hubble platform show which datasets to certify first.

## Key decisions
- Chose a single north-star metric — percentage of queries hitting certified assets — to align producers (certify what's heavily used) and consumers (query only certified data).
- Made accountability automatic via DPI generation on test failure rather than relying on manual escalation.
- Formalized producer-consumer expectations as contracts instead of tribal knowledge, fixing the communication breakdown behind pipeline breaks.
- Ran it as an organization-wide initiative with executive buy-in and measurable targets rather than a platform-team side project.

## Stack
Signals Marketplace certification system, data contracts with SLOs, automated quality tests generating Data Production Incidents, Hubble platform dashboards for usage and prioritization.

## Results
- 75% of queries now hit certified assets.
- 400% year-over-year increase in deprecated tables as redundant data was retired.
- 58% reduction in P80 datasets (the top-80%-usage set), cutting redundancy.
- Improved cross-domain reuse, e.g., weather IoT data shared across teams.

## Takeaways
Certification turns data mesh from philosophy into an operating model: ownership, contracts, and automated incidents create trust that makes decentralization workable. A single well-chosen usage-based metric can drive both supply-side (certification) and demand-side (query behavior) change, and executive sponsorship is a prerequisite, not a nice-to-have.
