---
id: cs1854
title: "Airbnb — Data Quality at Airbnb, Part 1: Rebuilding at Scale"
company: Airbnb
primary_category: data
sub_category: data-quality
year: 2020
source_url: https://medium.com/airbnb-engineering/data-quality-at-airbnb-e582465f3ef7
tags: [data-quality, spark, data-modeling, ownership, governance, midas]
---

# Airbnb — Data Quality at Airbnb, Part 1: Rebuilding at Scale
**Airbnb** · 2020 · [source](https://medium.com/airbnb-engineering/data-quality-at-airbnb-e582465f3ef7)

## Problem
Airbnb's rapid growth left its data infrastructure fragmented: datasets were owned by no one in particular, quality was inconsistent, and analysts spent significant time debugging unreliable data rather than deriving insights. The absence of clear ownership and standards made it impossible to trust the data underlying product decisions and experimentation.

## Approach / System design
Airbnb rebuilt its data foundation through a combination of organizational and technical changes. The Data Engineer role was reinstated as a dedicated function, and teams were reorganized into product-aligned pods where data engineers work alongside product and engineering counterparts. Pipelines were migrated from Hive to Spark and Scala for better reliability and expressiveness. Dataset-level SLAs, normalized data models, and a certification process called Midas were introduced to create a clear contract between producers and consumers.

## Key decisions
Decentralizing data ownership into product-aligned pods was a deliberate organizational choice, placing accountability with the teams that best understand the domain. The shift from Hive to Spark/Scala improved pipeline maintainability and performance. Midas certification was designed as a voluntary but valued standard to incentivize teams to invest in data quality.

## Stack
Apache Spark, Scala, Hive (legacy), Midas certification framework, internal SLA tooling.

## Results
Not covered in the source.

## Takeaways
Sustained data quality improvements require both organizational changes (clear ownership, dedicated roles) and technical scaffolding (SLAs, certification, normalized models) working together. Technical tooling alone is insufficient if teams do not feel accountable for the data they produce.
