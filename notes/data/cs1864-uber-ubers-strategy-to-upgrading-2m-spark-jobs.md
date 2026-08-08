---
id: cs1864
title: Uber — Uber's Strategy to Upgrading 2M+ Spark Jobs
company: Uber
primary_category: data
sub_category: data-quality
year: 2025
source_url: https://www.uber.com/us/en/blog/ubers-strategy-to-upgrading-2m-spark-jobs/
tags: [spark, migration, automation, piranha, shadow-testing, data-pipeline]
---

# Uber — Uber's Strategy to Upgrading 2M+ Spark Jobs
**Uber** · 2025 · [source](https://www.uber.com/us/en/blog/ubers-strategy-to-upgrading-2m-spark-jobs/)

## Problem
Uber needed to migrate over two million Spark jobs from version 2.4 to version 3.3 to access performance improvements and continued community support. The scale of the migration made manual code changes infeasible, and behavioral differences between Spark versions meant that automated upgrades risked silently changing output data, which could corrupt downstream models and reports without any compile-time error.

## Approach / System design
Uber executed the migration in four phases. The binary phase validated that jobs could run at all on the new version. The ecosystem phase updated dependencies. The source phase used Polyglot Piranha, an automated code refactoring tool, to apply Spark API changes across the codebase at scale. The final phase, called Iron Dome, used shadow data validation—running both old and new Spark versions on the same inputs and comparing outputs—to detect semantic regressions before cutover.

## Key decisions
Using Polyglot Piranha for automated source-level refactoring rather than manual rewrites was the only practical path to handling millions of jobs. The Iron Dome shadow validation phase was critical for catching behavioral differences that would have been invisible to static analysis or unit tests.

## Stack
Apache Spark (2.4 and 3.3), Polyglot Piranha (automated code refactoring).

## Results
The migration automated approximately 85% of the two million jobs and achieved roughly 50% reductions in both runtime and resource consumption after the Spark 3.3 upgrade.

## Takeaways
Large-scale framework migrations at this size require automation at every phase: dependency updates, source transformations, and output validation cannot be handled manually. Shadow testing that compares data outputs side-by-side is the most reliable technique for catching version-induced semantic regressions in data pipelines, where correctness is defined by output values rather than code behavior.
