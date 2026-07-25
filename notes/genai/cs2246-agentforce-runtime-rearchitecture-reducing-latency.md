---
id: cs2246
title: "Agentforce Runtime Rearchitecture: Reducing Latency"
company: Salesforce
primary_category: genai
sub_category: agents
year: 2026
source_url: https://www.salesforce.com/blog/agentforce-reducing-latency/
tags: [agentforce, latency, runtime-optimization, agentic-ai, llm-serving]
---

# Agentforce Runtime Rearchitecture: Reducing Latency
**Salesforce** · 2026 · [source](https://www.salesforce.com/blog/agentforce-reducing-latency/)

## Problem
Agentforce agent responses were taking as long as 20 seconds end to end, a level of latency that made urgent remediation necessary for the platform.

## Approach / System design
Over roughly six months, the team ran a comprehensive architectural review of the entire Agentforce 360 runtime and shipped more than 30 system-wide enhancements spanning both the platform and infrastructure layers, rather than isolated point fixes. The Atlas Reasoning Engine was refactored, the input-safety path was redesigned, topic classification was moved to a purpose-built small model, and serving infrastructure was upgraded, all backed by new performance monitoring dashboards to prevent regressions.

## Key decisions
- Cut the number of LLM calls before streaming the first output to the user from four to two, directly improving time-to-first-token.
- Replaced LLM-based input safety screening with an enhanced framework of deterministic rule filters plus variable isolation to defend against prompt injection without an extra model call.
- Introduced HyperClassifier, a proprietary small language model trained for single-token prediction instead of free-form generation, for topic classification.
- Moved to OpenAI's Scale Tier for premium latency and higher reliability.

## Stack
Atlas Reasoning Engine (refactored); HyperClassifier custom SLM; Data Cloud 360; OpenAI Scale Tier; enhanced performance-monitoring dashboards.

## Results
70% overall latency reduction; 30x speedup in topic classification via HyperClassifier while maintaining accuracy parity with larger models.

## Takeaways
Large latency wins came from systematic optimization across many components — reasoning-engine call structure, safety pipeline, classification, and serving tier — rather than any single fix. Continuous monitoring infrastructure is what keeps the gains from regressing.
