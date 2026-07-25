---
id: cs2106
title: "Tangle: An open-source ML experimentation platform built for scale"
company: Shopify
primary_category: data
sub_category: data-pipeline
year: 2025
source_url: https://shopify.engineering/tangle
tags: [ML pipeline, experimentation, content-based caching, open-source, Spark, Kubernetes]
---

# Tangle: An open-source ML experimentation platform built for scale
**Shopify** · 2025 · [source](https://shopify.engineering/tangle)

## Problem
Shopify's Search & Discovery team was losing significant time to reproducibility and data-engineering overhead in ML experimentation: queries tracked manually across experiments, piles of unstructured notebooks, the same data preparation repeated over and over, past results that could not be recreated, slow deployment cycles, and no good way to share work across the team.

## Approach / System design
Tangle is a platform-agnostic experimentation platform built from three layers: Components (reusable YAML-defined units that wrap containerized CLI programs in any language), Tasks (component instances configured with specific arguments), and Pipelines (DAGs of tasks where outputs feed downstream inputs). A visual drag-and-drop editor lets users assemble pipelines without parsing code. Data flows between tasks as files uploaded to and retrieved from storage rather than in-memory objects, so execution can be distributed without a shared runtime. Artifact histories are immutable, which underpins reproducibility.

## Key decisions
- Content-based caching instead of lineage-based caching: cache keys derive from output content hashes, so downstream tasks reuse identical results even when an upstream component's code changed, and artifacts are shared globally across team members — including from still-running executions.
- Language-neutral components: any CLI program (Python, JavaScript, Shell, C++, Java, Rust, Go, R, ...) can be a component without framework-specific rewrites.
- File-based inter-task communication for distributed execution.
- Optional typing: type metadata powers tooling without runtime enforcement, avoiding validation overhead and dependency conflicts.

## Stack
Docker/Podman for local execution, HuggingFace Spaces for multi-tenant deployment, per-tenant SQLite databases, cloud storage integration (GCS, S3), and a web-based visual pipeline editor.

## Results
A 10-hour pipeline completed in 20 minutes when one component changed but its outputs were content-identical. Post-deployment, Shopify reports more than a year of cumulative compute time saved, with thousands of redundant compute hours eliminated monthly through global caching.

## Takeaways
Decoupling reproducibility from any specific ML framework — via declarative YAML components around arbitrary containers — enables broad adoption. Content-aware caching beats lineage tracking for heterogeneous ML workloads, and visual pipelines with immutable artifact history open experimentation to people beyond specialized engineers.
