---
id: cs2236
title: A Human-Augmenting Agentic Workflow for Causal Inference
company: Netflix
primary_category: genai
sub_category: agents
year: 2026
source_url: https://netflixtechblog.com/a-human-augmenting-agentic-workflow-for-causal-inference-4623f0a9c5af
tags: [causal-inference, agentic-workflow, human-in-the-loop, data-science, experimentation]
---

# A Human-Augmenting Agentic Workflow for Causal Inference
**Netflix** · 2026 · [source](https://netflixtechblog.com/a-human-augmenting-agentic-workflow-for-causal-inference-4623f0a9c5af)

## Problem
Observational causal inference (OCI) demands deep domain expertise and careful judgment, but much of the work is repetitive and error-prone: checking covariate balance, running sensitivity analyses, and tracking many analysis iterations. Netflix wanted agents to absorb that toil while humans retained oversight, since validity cannot be checked against ground truth in observational settings.

## Approach / System design
Netflix built a three-persona orchestration framework: a Principal supplies the initial analysis plan, context, tools, and data; an Actor refines the plan into executable specifications and runs diagnostics; a Critic identifies gaps, assesses credibility, and suggests improvements. The actor-critic loop is grounded in target trial emulation — asking what ideal randomized experiment would answer each causal question. Four design diagnostics assess validity: covariate balance (standardized mean difference below 0.2), overlap (propensity scores between 0.1 and 0.9), placebo outcomes, and sensitivity to hidden confounders. Diagnostic failures trigger remediation playbooks, e.g. Crump-style trimming for poor overlap. Agents emit inspectable artifacts — plans, specifications, plots, executed notebooks — so humans can audit and re-execute everything, and the workflow can orchestrate multiple related analyses with consistent population definitions.

## Key decisions
- Process audits over outcome evaluation, since observational data offers no ground truth to score against.
- Every agent step produces human-inspectable, re-executable artifacts rather than opaque conclusions.
- Diagnostic-driven remediation playbooks codify what an expert would do when a validity check fails.
- Extensive domain-specific scaffolding instead of relying on one-shot general LLM capability.

## Stack
Claude Sonnet 4.6 as the LLM backbone; the open-sourced oci-agent repository built on EconML; doubly robust learning for effect estimation; version control and file storage for executed notebooks.

## Results
Benchmarked against the 2016 Atlantic Causal Inference Conference competition (44 competitor methods), the workflow achieved competitive RMSE and well-calibrated 95% confidence intervals (roughly 95% coverage across data-generating processes). With scaffolding it recovered ground truth in 9 of 10 test ACIC datasets; without scaffolding, one-shot prompting produced consistently incorrect, uncorrelated estimates. The Critic agent reliably separated satisfactory estimates (lower RMSE, better calibration) from unsatisfactory ones.

## Takeaways
Agentic workflows for specialized analytical work need serious scaffolding — general-purpose LLM ability alone yields unreliable results. In domains without ground truth, process transparency and human-in-the-loop review substitute for outcome validation. The human-augmenting framing reduces toil while preserving expert judgment where it matters.
