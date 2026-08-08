---
id: cs1862
title: Uber — Sparkle: Standardizing Modular ETL at Uber
company: Uber
primary_category: data
sub_category: data-pipeline
year: 2024
source_url: https://www.uber.com/blog/sparkle-modular-etl/
tags: [etl, spark, modular, testing, yaml, jinja, data-pipeline]
---

# Uber — Sparkle: Standardizing Modular ETL at Uber
**Uber** · 2024 · [source](https://www.uber.com/blog/sparkle-modular-etl/)

## Problem
Uber's data engineering teams maintained large numbers of Spark ETL pipelines written in a variety of styles, making pipelines hard to reuse, test, or hand off between teams. Business logic was interleaved with execution boilerplate, testing was inconsistent, and migrating from Hive to Spark required rewriting pipelines individually.

## Approach / System design
Sparkle is a Spark-based modular ETL framework that separates business logic from execution infrastructure. Business logic is expressed as SQL or procedural blocks, wired together via YAML configuration files that use Jinja templating for parameterization. A built-in testing framework enables unit and integration tests to be written alongside pipeline definitions without additional tooling setup. The framework compiles YAML declarations into optimized Spark execution plans.

## Key decisions
Choosing YAML with Jinja templating rather than a custom DSL kept the learning curve low while providing enough expressiveness for complex pipeline configurations. Building the testing framework as a core part of the framework rather than a separate tool made testing the default path rather than an optional add-on.

## Stack
Apache Spark, YAML, Jinja templating.

## Results
Sparkle delivered approximately 30% productivity gains for data engineering teams and achieved more than 5x performance improvements over equivalent Hive pipelines.

## Takeaways
Separating business logic from execution details in ETL frameworks pays significant dividends in reusability and testability, particularly in large organizations where pipelines change hands frequently. Standardizing on a single framework across teams enables cross-team code review, shared optimization, and easier platform-wide migrations.
