---
id: cs1860
title: Spotify — Data Platform Explained Part II
company: Spotify
primary_category: data
sub_category: data-quality
year: 2024
source_url: https://engineering.atspotify.com/2024/5/data-platform-explained-part-ii
tags: [data-platform, event-delivery, pipelines, gcp, lineage, data-quality]
---

# Spotify — Data Platform Explained Part II
**Spotify** · 2024 · [source](https://engineering.atspotify.com/2024/5/data-platform-explained-part-ii)

## Problem
Spotify generates over one trillion events per day across its products and runs more than 38,000 scheduled data pipelines. Ensuring that this volume of data is reliably delivered, correctly retained, properly access-controlled, and traceable through lineage requires platform-level abstractions that individual teams cannot be expected to build independently.

## Approach / System design
Spotify's data platform runs on Google Cloud Platform and provides centralized primitives for event delivery, pipeline scheduling, retention policies, access controls, data lineage, and quality checks. The platform embeds these concerns into the infrastructure layer so that teams inheriting it automatically gain compliance with Spotify's data governance standards. Community practices and internal tooling drove adoption across product and analytics teams.

## Key decisions
Running on GCP and leveraging managed services for core infrastructure allowed Spotify to focus engineering investment on the platform abstractions rather than database and storage operations. Making lineage and quality checks platform-level features rather than opt-in libraries ensured consistent coverage across the majority of pipelines.

## Stack
Google Cloud Platform (GCP), internal pipeline scheduler, event delivery infrastructure.

## Results
The platform handles over one trillion events per day and schedules more than 38,000 data pipelines.

## Takeaways
Data platform adoption is as much a social and organizational challenge as a technical one: community practices, documentation, and internal examples matter as much as the underlying infrastructure. Embedding governance primitives—lineage, quality, access control—at the platform layer rather than the application layer dramatically reduces the gap between what is possible and what is actually enforced.
