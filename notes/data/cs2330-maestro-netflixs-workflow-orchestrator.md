---
id: cs2330
title: Maestro: Netflix's Workflow Orchestrator
company: Netflix
primary_category: data
sub_category: data-pipeline
year: 2024
source_url: https://netflixtechblog.com/maestro-netflixs-workflow-orchestrator-ee13a06f9c78
tags: [workflow-orchestration, data-pipeline, ML-pipeline, open-source, DAG, distributed-systems]
---

# Maestro: Netflix's Workflow Orchestrator
**Netflix** · 2024 · [source](https://netflixtechblog.com/maestro-netflixs-workflow-orchestrator-ee13a06f9c78)

## Problem
Netflix runs deeply interconnected data and ML workflows — ETL pipelines, model training, A/B test pipelines, cross-storage data movement — for thousands of users, applications, and services. Splitting workflows across multiple orchestration clusters adds coordination complexity and degrades UX; since Netflix's tables live in a single data warehouse, one orchestrator must handle everything, at ever-growing scale, and support non-engineers as well as engineers.

## Approach / System design
Maestro is a horizontally scalable, fully managed workflow orchestrator providing Workflow-as-a-Service, now open-sourced:
- **Workflow model**: JSON workflow definitions with two sections — properties (author/owner, run strategy, concurrency, triggering/alerting; preserved across versions) and versioned workflow (id, metadata, timeout, criticality levels; every change creates a new version for tracking and reversion). Steps carry types, parameters, dependencies, retry policies, and failure modes. Business logic can be packaged as Docker images, notebooks, bash, SQL, Python, and more. Unlike DAG-only orchestrators, Maestro supports both acyclic and cyclic workflows.
- **Run strategies**: sequential (FIFO default), strict sequential (queue blocks on a failure until manually unblocked), first-only, last-only (stop the running instance in favor of the newest — for latest-snapshot processing), and parallel with a concurrency limit (e.g., backfills).
- **Parameters and SEL**: dynamic parameters with code injection are supported through a homemade Simple, Secure, and Safe Expression Language — a JLS-subset parser with parse-time validation, Java Security Manager restrictions, and runtime limits (loop iterations, array sizes, object memory) to prevent abuse like OOM-inducing loops. Output parameters flow back via REST so step runtimes never touch the Maestro database.
- **Execution patterns**: foreach (each iteration internally a separate workflow instance, scaling to hundreds of thousands of iterations), conditional branches (SEL-evaluated), and subworkflows ("workflow as a function"), composable into patterns like auto-recovery pipelines.
- **Step runtime**: an interface defining start/execute/terminate plus runtime state and execution results; step parameters are assembled through a defined merge order (defaults → injected → typed defaults → workflow/step info → new params → definition params → run/restart overrides).
- **Signals and dependencies**: steps declare data conditions via signals (messages carrying parameter values, published by step outputs or external systems like SNS/Kafka), with signal matching, comparison operators, signal lineage navigation, and exactly-once triggering for signal-subscribed workflows.
- **Operability**: step-level breakpoints (pause/resume like an IDE), execution timelines of state-machine events, platform-vs-user retry policies with backoff, aggregated views merging state across runs, and rollup summaries that flatten nested subworkflows/foreach into leaf-step status counts (eventually consistent).
- **Eventing**: internal lifecycle events are processed in-queue and selectively transformed into external events (SNS, Kafka) for event-driven downstream services, covering workflow changes and instance status changes.

## Key decisions
- One horizontally scalable orchestrator for all of Netflix rather than sharded clusters, because workflows are interconnected and share one warehouse.
- Build a custom sandboxed expression language (SEL) instead of allowing arbitrary code injection or pushing logic into user code.
- Model foreach iterations as internal workflow instances so loops scale like ordinary workflows.
- Distinguish platform retries from user retries, with configurable policies and zero-retry options for non-idempotent steps.
- Keep step runtimes isolated from the database, communicating output parameters only via REST API.

## Stack
Java-based engine (SEL follows Java Language Specification, Java Security Manager), JSON workflow definitions, internal queue plus SNS/Kafka external eventing, REST API, support for Docker/notebook/bash/SQL/Python step payloads. Open-sourced at github.com/Netflix/maestro.

## Results
- Hundreds of thousands of workflows migrated to Maestro with minimal interruption.
- 87.5% year-over-year increase in executed jobs; thousands of workflow instances launched daily; ~500K jobs/day on average and roughly 2 million jobs completed on peak days.
- Serves thousands of end users, applications, and services; complex production workflows include hundreds of subworkflows spanning tables owned by multiple teams.

## Takeaways
- At sufficient scale, orchestration is a multi-tenant platform product: run strategies, breakpoints, timelines, and rollups exist because thousands of non-experts operate workflows.
- Safe parameterization is the linchpin — parameterized workflows hit the sweet spot between rigid static definitions and unmanageable fully dynamic ones, but require a sandboxed language to be safe.
- Signals decouple producers from consumers with exactly-once triggering, replacing polling and cron coupling between teams' pipelines.
- Supporting cyclic graphs and composable patterns (foreach, subworkflow, conditionals) in the engine beats forcing users to emulate them atop a DAG-only model.
