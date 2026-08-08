---
id: cs1855
title: "Airbnb — Data Quality at Airbnb, Part 2: A New Gold Standard"
company: Airbnb
primary_category: data
sub_category: data-quality
year: 2020
source_url: https://medium.com/airbnb-engineering/data-quality-at-airbnb-870d03080469
tags: [data-quality, midas, certification, sla, governance, data-contracts]
---

# Airbnb — Data Quality at Airbnb, Part 2: A New Gold Standard
**Airbnb** · 2020 · [source](https://medium.com/airbnb-engineering/data-quality-at-airbnb-870d03080469)

## Problem
After rebuilding the organizational and technical foundations described in Part 1, Airbnb needed a concrete, company-wide definition of what "high-quality data" actually means. Without a shared standard, different teams applied different criteria, making it impossible to consistently identify and promote the datasets that the entire company could rely on.

## Approach / System design
Airbnb formalized the Midas certification program as a company-wide gold standard for datasets. Certification is evaluated across six quality dimensions: accuracy, consistency, timeliness, cost, usability, and availability. A dataset seeking Midas status passes through a structured nine-step design-and-review process involving the owning team, data consumers, and a review board. Certified datasets are prominently surfaced in internal tooling to guide analysts toward trusted sources.

## Key decisions
Defining six explicit dimensions rather than a single pass/fail quality score makes it possible to have targeted conversations about which dimension is failing and what remediation is required. The nine-step process creates deliberate checkpoints that catch design and documentation gaps before a dataset enters wide use. Making Midas status visible in discovery tools creates a market incentive for teams to pursue certification.

## Stack
Midas certification framework, internal data discovery and governance tooling.

## Results
Not covered in the source.

## Takeaways
A well-defined multi-dimensional certification standard, combined with a structured review process, is more effective at raising data quality across an organization than ad-hoc checks or monitoring alone. Making certification status discoverable turns quality into a shared organizational value rather than an engineering concern.
