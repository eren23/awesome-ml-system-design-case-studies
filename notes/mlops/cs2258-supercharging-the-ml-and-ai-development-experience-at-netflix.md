---
id: cs2258
title: Supercharging the ML and AI Development Experience at Netflix
company: Netflix
primary_category: mlops
sub_category: efficiency
year: 2025
source_url: https://netflixtechblog.com/supercharging-the-ml-and-ai-development-experience-at-netflix-b2d5b95c63eb
tags: [metaflow, orchestration, workflow, developer-experience, kubernetes, maestro, productivity]
---

# Supercharging the ML and AI Development Experience at Netflix
**Netflix** · 2025 · [source](https://netflixtechblog.com/supercharging-the-ml-and-ai-development-experience-at-netflix-b2d5b95c63eb)

## Problem
ML/AI development differs from traditional software: state (data, models) is large, mutable, and expensive to compute. Practitioners want notebook-like fast iteration with preserved state, but inside a production-grade workflow framework. Metaflow's existing `resume` command re-executes from a checkpoint onward, which still adds latency between iterations.

## Approach / System design
Netflix added **Spin** to Metaflow as a third execution mode alongside `run` (full execution with versioning/metadata) and `resume` (restart from a checkpoint). Spin executes a single workflow step in isolation, inheriting parent state from persisted artifacts, and skips metadata tracking for throwaway iterations. Steps act as checkpoint boundaries with automatic artifact persistence, so state transfers seamlessly between iterations. The same post covers the surrounding ecosystem: Maestro (Netflix's workflow orchestrator, now open-sourced) for production scheduling, and Metaflow's path from local development to scaled execution on AWS Batch, Titus, and Kubernetes.

## Key decisions
- Skip tracking during Spin runs — throwaway iterations should not pollute metadata.
- Allow input/output artifact injection via Python modules, effectively enabling unit testing of individual steps.
- Optional persistence flag for selectively storing Spin artifacts.
- IDE and agent integration: a VS Code extension with keyboard shortcuts, plus markdown instructions so AI coding agents can use Spin for rapid step-level testing.

## Stack
Metaflow (2.19), Maestro and Argo Workflows for orchestration, AWS Batch / Titus / Kubernetes as compute platforms, Metaflow Cards for visualization, VS Code/Cursor extensions, Runner and Client APIs.

## Results
Qualitative rather than quantitative: demonstrated single-step iteration workflows, faster error surfacing (e.g., catching a stratified-sampling bug), and successful use of Spin by a Claude Code agent for rapid testing. Specific speedup numbers are not covered in the source.

## Takeaways
Bringing notebook-style iteration speed into a production workflow framework — rather than forcing a choice between the two — is the developer-experience unlock. Step-level execution with state inheritance benefits humans and AI coding agents alike, and composability with existing features (cards, configs, decorators) matters more than standalone tooling.
