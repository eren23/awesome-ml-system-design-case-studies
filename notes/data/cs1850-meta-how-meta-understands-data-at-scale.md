---
id: cs1850
title: Meta — How Meta Understands Data at Scale
company: Meta
primary_category: data
sub_category: data-discovery
year: 2025
source_url: https://engineering.fb.com/2025/04/28/security/how-meta-understands-data-at-scale/
tags: [data-classification, cataloging, metadata, schematization, privacy-aware-infrastructure]
---

# Meta — How Meta Understands Data at Scale
**Meta** · 2025 · [source](https://engineering.fb.com/2025/04/28/security/how-meta-understands-data-at-scale/)

## Problem
Meta operates hundreds of data systems containing millions of data assets, making it practically impossible for teams—or privacy reviewers—to manually understand what data exists, what it means, and what privacy properties it carries. Without a systematic way to make data understandable, privacy governance and compliance become bottlenecks or gaps.

## Approach / System design
Meta's Privacy Aware Infrastructure addresses this through a multi-stage pipeline: schematization gives raw data a structured form, ML-based classification automatically assigns privacy-relevant labels using a universal privacy taxonomy, annotation enriches assets with human-readable metadata, and OneCatalog provides a unified inventory spanning hundreds of systems. Together these steps transform opaque data stores into a queryable, privacy-annotated catalog.

## Key decisions
Using ML classification rather than purely manual annotation was critical to achieving coverage at scale. Adopting a universal privacy taxonomy creates a consistent semantic layer across otherwise incompatible systems, enabling cross-system privacy policies to be expressed and enforced uniformly.

## Stack
Not covered in the source.

## Results
Not covered in the source.

## Takeaways
Building shared data understanding is a prerequisite for automated privacy enforcement: you cannot control what you cannot identify. A combination of structural schematization and ML-assisted classification enables catalog coverage at a scale that human annotation alone cannot sustain.
