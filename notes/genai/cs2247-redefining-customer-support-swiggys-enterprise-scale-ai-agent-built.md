---
id: cs2247
title: "Redefining Customer Support: Swiggy's Enterprise-Scale AI Agent Built on Databricks"
company: Swiggy
primary_category: genai
sub_category: rag
year: 2025
source_url: https://www.databricks.com/blog/redefining-customer-support-swiggys-enterprise-scale-ai-agent-built-databricks
tags: [customer-support, enterprise-agent, databricks, llm, multi-agent]
---

# Redefining Customer Support: Swiggy's Enterprise-Scale AI Agent Built on Databricks
**Swiggy** · 2025 · [source](https://www.databricks.com/blog/redefining-customer-support-swiggys-enterprise-scale-ai-agent-built-databricks)

## Problem
Swiggy's rule-based customer support could not scale with the delivery platform's growth: it couldn't absorb demand spikes, offered no personalization, and its rigid workflows produced generic responses to complex inquiries. Swiggy wanted always-on instant support, maximal query automation, reduced dependence on human agents, and lower average handling time.

## Approach / System design
Swiggy and Databricks iterated through phases: two-tier intent classification with LLM responses; RAG for contextual retrieval; a transition to agentic AI for stateful multi-turn conversations; LLM evaluation and selection in the Databricks AI Playground; agent tuning via prompt engineering (Meta-prompting, ReAct, chain-of-thought); a multi-agent architecture segregating function by support disposition; and systematic MLflow-based evaluation. CRM integration uses structured action-triggers so agent decisions drive backend actions.

## Key decisions
- One LLM family chosen for naturally conversational output over alternatives needing heavy prompt tuning.
- Separate agent instances per disposition for quality and maintainability rather than one agent handling everything.
- Hybrid routing combining LLM assignment with rule-based routing for higher accuracy.
- Tiered model strategy: simple models for routine queries, reasoning models for complex cases.
- Prompt engineering over fine-tuning — catastrophic-forgetting risk outweighed the benefits.
- Granular real-time tracing of every agent step.

## Stack
Databricks AI Playground, Model Serving, and MLflow 3.0 (tracing, prompt registry, built-in and custom judges); AI Gateway guardrails for permissions, rate limiting, and payload logging; Unity Catalog for asset governance; structured action-trigger CRM integration.

## Results
Sub-second latency across thousands of concurrent sessions; 100% automation of targeted customer queries without human intervention; improved customer satisfaction and reduced operational cost on high-frequency, low-complexity inquiries. Targets: p99 latency under 500ms and accuracy above 99%.

## Takeaways
Functional segregation across agents beats a single agent on multi-intent conversations. Don't over-rely on short-term memory — prompt agents to refresh data via tool calls. Prompt-level cost optimization (removing emojis, trimming examples) cut inference cost without semantic loss, and autoscaling from near-zero to hundreds of nodes is essential for variable 24/7 traffic.
