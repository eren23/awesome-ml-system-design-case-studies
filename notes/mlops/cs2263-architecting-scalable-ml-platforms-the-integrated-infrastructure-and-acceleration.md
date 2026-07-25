---
id: cs2263
title: "Architecting Scalable ML Platforms: The Integrated Infrastructure and Acceleration Behind Rovo"
company: Atlassian
primary_category: mlops
sub_category: platform
year: 2025
source_url: https://www.atlassian.com/blog/how-we-build/architecting-scalable-ml-platforms
tags: [ml-platform, gpu-cluster, workflow-orchestration, governance, rovo, llm, modular-ml, data-governance]
---

# Architecting Scalable ML Platforms: The Integrated Infrastructure and Acceleration Behind Rovo
**Atlassian** · 2025 · [source](https://www.atlassian.com/blog/how-we-build/architecting-scalable-ml-platforms)

## Problem
Atlassian's ML infrastructure was fragmented and tightly coupled, slowing experimentation and creating compliance and reliability bottlenecks. Distributed teams building products like Rovo Search and Chat needed to iterate on ML systems quickly while enforcing strict data governance across a very large data estate.

## Approach / System design
ML Studio, Atlassian's unified ML platform, rests on three pillars:
1. **Composable ML modules** — self-contained, versioned, shareable components combinable into pipelines; every code push yields a buildable artifact tied to Git.
2. **Workflow orchestrator** — a central service for scheduling and automation, launchable from a portal, CLI, or APIs, supporting nested workflows, hot clusters, and cron scheduling.
3. **Embedded compliance controls** — a multi-layer governance framework: identity-based access, domain-level controls, and column-level data classification with automatic tag propagation.

The platform integrates with feature stores, experiment trackers, model registries, deployment targets, and monitoring (ML Lens for regression detection).

## Key decisions
- Invest in local development loops with remote developer support — Python module builds dropped from minutes to under 30 seconds.
- Automatic caching that detects unchanged task parameters and reuses prior results.
- "Experimental workflows" that permit PR-free rapid iteration with direct dataset access, trading ceremony for speed inside guardrails.
- Automate governance (column-level classification with tag propagation) instead of relying on manual review, so compliance scales with the platform.

## Stack
Databricks for training with GPU cluster acceleration; Git-based module versioning and artifact management; ML Studio's own orchestrator, portal, and CLI; ML Lens monitoring.

## Results
- Backs Rovo features serving 5M+ monthly active users.
- 900k+ datasets under access control; ~120k monthly workflow runs by 100+ teams; ~20k monthly model iterations; 2k+ reusable modules.
- ~1,000 hours/month saved via caching (80% of workflows use it daily) and 100+ hours/day saved via experimental workflows.

## Takeaways
Modularity plus integrated, automated governance is what allows velocity at enterprise scale — the two are not in tension if compliance is built into the platform layers. The largest productivity wins came from unglamorous friction removal: fast local builds, result caching, and letting experiments skip the PR cycle.
