---
id: cs2400
title: "Meson: Workflow Orchestration for Netflix Recommendations"
company: Netflix
primary_category: mlops
sub_category: efficiency
year: 2021
source_url: https://netflixtechblog.com/meson-workflow-orchestration-for-netflix-recommendations-fc932625c1d9
tags: [workflow orchestration, ml pipeline, recommendations, pipeline management, dag, scheduling]
---

# Meson: Workflow Orchestration for Netflix Recommendations
**Netflix** · 2021 · [source](https://netflixtechblog.com/meson-workflow-orchestration-for-netflix-recommendations-fc932625c1d9)

## Problem
Netflix runs many ML workflows daily to build, train, and validate the personalization algorithms behind video recommendations. These pipelines span heterogeneous technologies, and the team needed to orchestrate them reliably, use cluster resources efficiently, and raise the velocity, reliability, and repeatability of algorithmic experiments.

## Approach / System design
Meson is a general-purpose workflow orchestration and scheduling framework that manages the full ML pipeline lifecycle. Workflows are DAGs supporting parallel branches and conditional joins, with data flow and runtime context passed between steps. A single workflow can mix Spark jobs, Python, R, and Docker-based steps. Meson runs as a framework on Apache Mesos, which provides resource scheduling and task isolation, with a custom executor keeping a live channel between scheduler and tasks.

## Key decisions
- Apache Mesos for resource management, but with a pluggable scheduler abstraction so Meson isn't married to it.
- A custom Mesos executor enabling heartbeats, progress updates, and rich data passing beyond exit codes.
- A Scala-based DSL for defining workflows with operators for sequencing, parallelism, and looping — ML constructs like parameter sweeps are first-class.
- A purpose-built extension architecture for custom step types: Spark Submit, Hive queries, microservice callouts, Docker steps.
- Workflow outputs treated as first-class artifacts, enabling smarter retries and custom visualization.

## Stack
Apache Mesos, Spark/MLlib, Scala (DSL), Python, R, Docker, Cassandra (persistence).

## Results
The system supports large-scale experimentation — e.g., parameter sweeps fanning out into tens of thousands of Docker containers. Specific deployment-scale or performance benchmarks are not given in the post.

## Takeaways
- ML orchestration must be polyglot: real pipelines mix Spark, scripting languages, and containers, and the orchestrator has to treat that as normal.
- Richer executor–scheduler communication than "exit code" pays off in observability and control.
- Building extensibility in early proved critical as adoption spread beyond the original recommendations use case.
