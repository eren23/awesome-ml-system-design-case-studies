---
id: cs2108
title: Introducing Configurable Metaflow
company: Netflix
primary_category: data
sub_category: data-pipeline
year: 2024
source_url: https://netflixtechblog.com/introducing-configurable-metaflow-d2fb8e9ba1c6
tags: [Metaflow, ML workflow, configuration management, MLOps, deployment, Python]
---

# Introducing Configurable Metaflow
**Netflix** · 2024 · [source](https://netflixtechblog.com/introducing-configurable-metaflow-d2fb8e9ba1c6)

## Problem
Netflix teams operate thousands of Metaflow ML/AI pipelines, and a recurring pain point was deploying multiple variants of the same flow with different configurations without touching the source code. Existing workarounds — JSON Parameters, IncludeFile, or bespoke config plumbing — were awkward and, crucially, could not configure decorators such as `@resources` or `@schedule`, since Parameters only resolve when a run starts.

## Approach / System design
The ML Platform team added a first-class Config construct to Metaflow (shipped in 2.13), complementing Parameters and Artifacts. Unlike Parameters, Configs are resolved and persisted at deployment time, which lets them drive decorator settings and step behavior before any execution begins. Configs behave like dictionary-style artifacts: they are automatically versioned and inspectable through the Client API alongside code, models, and execution environments. Internally, Netflix's Metaboost CLI uses config "bindings" to stamp out multiple flow variants from a single template — practitioners swap a YAML file to target a different metric instead of rewriting the pipeline.

## Key decisions
- Resolve configs at deployment time rather than run time, unlocking decorator configuration that Parameters cannot express.
- Support pluggable, user-defined parsers (TOML, YAML, Pydantic validation), including parsers specified as strings to avoid pulling remote dependencies.
- Integrate with inversion-of-control patterns: Configs compose with Hydra and the Runner/Deployer APIs so external orchestrators can drive parameter sweeps programmatically.
- Extract a low-level, un-opinionated primitive rather than prescribing a full config-management solution, keeping Metaflow's philosophy intact.

## Stack
Metaflow 2.13, TOML/YAML config formats, Pydantic validation, Hydra/OmegaConf for cascading configuration, and Netflix-internal tooling: Metaboost (CLI), Maestro (orchestrator), Kragle (data warehouse).

## Results
No quantitative metrics are given; the qualitative outcome is that teams can deploy and manage sets of related flows — differing in resources, schedules, and dependencies — from one codebase, and non-engineering stakeholders can spin up experiment variants by editing config files.

## Takeaways
Configuration management belongs at the framework level: making configs deployment-time, versioned artifacts removes boilerplate and makes flow variants cheap. Exposing a small composable primitive that works with existing config ecosystems (Hydra, Pydantic) scales better than a prescriptive solution.
