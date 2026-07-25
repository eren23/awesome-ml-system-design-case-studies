---
id: cs2335
title: How we cut our NLQ agent debugging time from hours to minutes with Agent Observability
company: Datadog
primary_category: genai
sub_category: agents
year: 2026
source_url: https://www.datadoghq.com/blog/llm-observability-at-datadog-nlq/
tags: [nlq, natural-language-query, agent-observability, llm, debugging, tracing, rag]
---

# How we cut our NLQ agent debugging time from hours to minutes with Agent Observability
**Datadog** · 2026 · [source](https://www.datadoghq.com/blog/llm-observability-at-datadog-nlq/)

## Problem
Datadog's Cloud Cost Management team built a natural language query (NLQ) agent that translates plain-English questions into metrics queries. Early evaluation was painful: naive exact-string comparison of generated queries against expected ones reported success rates as low as 2%, badly understating actual quality, and debugging a failure meant hours of manual side-by-side query comparison with little visibility into where in the pipeline the agent went wrong.

## Approach / System design
The team dogfooded Datadog's own Agent Observability product. Instead of a binary pass/fail check, they decomposed query correctness into five independently measurable dimensions — parsing validity, metric selection, roll-up aggregation, grouping logic, and filter application — and implemented each as a Python evaluator inside Agent Observability Experiments. Evaluators are organized hierarchically from strictest to most lenient, so a failure is categorized rather than lumped into a single "wrong" bucket. A ground-truth dataset was curated from real user testing traces rather than synthetic prompts, preserving genuine phrasing and behavior patterns. Distributed tracing over the agent's tool calls lets engineers inspect arguments and intermediate outputs at the span level instead of only the final query string. Experiments run automatically in CI/CD on every build, using local evaluation to save resources, with on-demand runs against staging and production.

## Key decisions
- Component-level evaluators over exact-match scoring, so failures become actionable diagnoses (e.g., filters identified as the primary error source while parsing and roll-up were consistently strong).
- Ground truth built from actual user traces, not synthetic prompts.
- Hierarchical evaluator ordering (strict checks upstream, lenient downstream) to classify failure modes.
- Trace-driven debugging via APM-integrated agent tracing rather than analyzing final outputs alone.
- Standardized datasets and evaluators so different models can be compared objectively without rebuilding the eval harness.

## Stack
Datadog Agent Observability (Experiments, LLM tracing), Python evaluators, APM-integrated distributed tracing, CI/CD-triggered experiment runs.

## Results
Debugging and analysis time dropped from hours to minutes. Component evaluation revealed that true agent performance was far higher than the misleading ~2% suggested by exact string comparison, and pinpointed filter application as the main weakness to fix.

## Takeaways
- Decomposing correctness into measurable dimensions turns ambiguous failures into targeted fixes.
- Real user-derived test data captures patterns synthetic prompts miss.
- Using the same observability platform for agent behavior and application signals removes tool fragmentation and speeds iteration.
- Consistent eval infrastructure makes model swaps and comparisons cheap.
