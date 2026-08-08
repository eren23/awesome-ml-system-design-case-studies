---
id: cs1859
title: Criteo — Scheduling Data Pipelines at Criteo, Part 2
company: Criteo
primary_category: data
sub_category: data-pipeline
year: 2022
source_url: https://medium.com/criteo-engineering/scheduling-data-pipelines-at-criteo-part-2-8b0da38ff3a4
tags: [data-pipeline, scheduler, bigdataflow, dag, sql, backfill]
---

# Criteo — Scheduling Data Pipelines at Criteo, Part 2
**Criteo** · 2022 · [source](https://medium.com/criteo-engineering/scheduling-data-pipelines-at-criteo-part-2-8b0da38ff3a4)

## Problem
Traditional workflow schedulers require engineers to explicitly declare task dependencies and DAG structure, which is tedious, error-prone, and diverges from the actual data lineage encoded in the SQL transformations themselves. At Criteo's scale, managing this manual layer of dependency configuration across hundreds of pipelines becomes a significant maintenance burden.

## Approach / System design
Criteo's BigDataFlow system applies ideas from database query planning to workflow orchestration. Rather than requiring engineers to declare dependencies, BigDataFlow parses the SQL in each pipeline step and infers task dependencies and partition schemas automatically from the data lineage embedded in the queries. The scheduler then uses these inferred dependencies to build DAGs, handle scheduling, manage data retention, and trigger backfills based on partition existence rather than time-based triggers.

## Key decisions
Deriving dependencies from SQL analysis rather than manual declarations ensures the declared DAG always matches the actual data flow, eliminating a common class of errors. Using partition existence as the scheduling trigger rather than wall-clock time makes pipelines data-driven and naturally handles late-arriving data. Incorporating backfill logic into the scheduler rather than treating it as a separate operational procedure reduces operational complexity.

## Stack
BigDataFlow (internal scheduler), SQL-based dependency inference, DAG construction engine, partition-based scheduling.

## Results
Not covered in the source.

## Takeaways
Applying query-planning techniques to workflow orchestration is a powerful way to reduce manual configuration and keep pipeline graphs consistent with actual data dependencies. Partition-driven scheduling is more resilient to data delays than time-driven scheduling, particularly in systems where upstream data arrival is variable.
