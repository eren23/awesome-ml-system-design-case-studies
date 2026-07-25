---
id: cs2125
title: Lyft Built a Self-Serve AI Agent Platform for Customer Support with LangGraph and LangSmith
company: Lyft
primary_category: genai
sub_category: agents
year: 2025
source_url: https://www.langchain.com/blog/lyft-built-a-self-serve-ai-agent-platform-for-customer-support-with-langgraph-and-langsmith
tags: [customer-support, langgraph, langsmith, multi-agent, dynamodb, checkpointing, deflection]
---

# Lyft Built a Self-Serve AI Agent Platform for Customer Support with LangGraph and LangSmith
**Lyft** · 2025 · [source](https://www.langchain.com/blog/lyft-built-a-self-serve-ai-agent-platform-for-customer-support-with-langgraph-and-langsmith)

## Problem
Each customer-support AI agent took roughly 6 months of dedicated ML-engineer work, with domain experts unable to ship changes without a technical intermediary. With demand surging across new user segments and issue types, the loop of expert definitions → MLE translation → code adjustment could not keep up.

## Approach / System design
Lyft built a multi-agent orchestration platform on LangGraph's router architecture: a meta-agent classifies incoming requests and dispatches to specialized subagents via `Command(goto=...)`, with separate router instances for riders and drivers and safety checks (malicious-intent and safety-issue detection) running in parallel on every turn. Agents come in two flavors — hand-built specialized agents for complex workflows, and configurable agents where domain experts author structured prompts and a `ConfigurableAgent` class assembles the graph, binds tools, and manages state at runtime. Conversation state persists through a custom `DynamoDBSaver` implementing LangGraph's `BaseCheckpointSaver`, enabling replay and debugging.

## Key decisions
- A configurable-agent layer so non-engineers can ship agents from structured prompt templates (role, scope, workflow phases, content guidelines).
- Treat prompt quality — not infrastructure — as the real bottleneck: a 5-component prompt framework, mandatory pre-activation review checklist, and an automated Git-backed CI prompt-validation pipeline.
- Custom DynamoDB checkpointing instead of in-memory state, so conversations survive restarts and can be replayed.
- 100% of production agents covered by automated LLM-as-a-Judge evaluation pipelines.

## Stack
LangGraph (subgraph/router architecture), LangSmith (tracing, dashboards, LLM-as-a-Judge evaluation, Prompt Hub), DynamoDB with custom checkpoint saver, PagerDuty alerting driven by LangSmith metrics, Git-backed CI for prompt validation.

## Results
Agent development time dropped from ~6 months to ~2 weeks for configurable agents; hallucination and contradiction rates fell 20%; AI resolution rate rose 16% since platform launch; and multiple non-engineering team members now independently build and iterate agents. Per the catalog metadata, the platform reached 270,000 monthly AI interactions with a 65% deflection rate across 7 production agents.

## Takeaways
Democratizing agent development through configuration works only with prompt discipline — prompts are product specifications, not code comments. Automated validation before deployment and multi-layered production monitoring (volume, latency, tokens, tool success, quality scores) matter more than the orchestration infrastructure itself.
