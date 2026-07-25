---
id: cs2230
title: How Rovo Embraces Multi-Agent Orchestration
company: Atlassian
primary_category: genai
sub_category: agents
year: 2025
source_url: https://www.atlassian.com/blog/atlassian-engineering/how-rovo-embraces-multi-agent-orchestration
tags: [multi-agent, orchestration, rovo, agentic-ai, enterprise]
---

# How Rovo Embraces Multi-Agent Orchestration
**Atlassian** · 2025 · [source](https://www.atlassian.com/blog/atlassian-engineering/how-rovo-embraces-multi-agent-orchestration)

## Problem
As Rovo Chat accumulated tools and capabilities, the single-agent design became unreliable: the agent struggled with queries spanning multiple domains and frequently picked the wrong tool. Exposing hundreds of tools to one agent didn't scale in quality or maintainability.

## Approach / System design
Atlassian rebuilt Rovo Chat as a hierarchical multi-agent framework with three layers: a top-level orchestrator that routes queries to reasoning modes and system tools; domain-specialized subagents (e.g., a Jira Agent for ticket queries); and simple system tools that bypass agent overhead for basic tasks. The orchestrator supports three reasoning modes — brainstorming (LLM-only, low latency), tool QnA (single parallel tool calls), and reasoning (multi-step sequences with explicit planning). The team first tried a graph-based DAG orchestrator, then reverted to a hybrid tool-loop model in which the LLM dynamically selects one layer of tools at a time, which recovers better from failures.

## Key decisions
- Hierarchical structure over a flat tool list: grouping tools into domain subagents reduces tool-selection confusion and contains the blast radius of adding new tools.
- Three explicit reasoning modes so simple queries stay fast while complex ones get multi-step planning.
- Hybrid tool-loop orchestration over a rigid DAG: dynamic one-layer-at-a-time tool selection beat precommitted execution graphs on both quality and latency.
- Domain-specific machinery inside subagents: JQL integration with specialized instructions, entity linking to map named entities to user IDs, and batch loops for handling 1000+ Jira issues.

## Stack
Jira Query Language (JQL) integration, entity linking, batch processing loops for large Jira result sets, and LLM-as-judge evaluation against curated reference answers.

## Results
Versus the single-agent baseline, the hybrid orchestrator improved quality by +3.49% (DAG: +2.52%) while cutting latency: P10 -75.96%, P50 -29.5%, P90 -19.97%. The DAG variant improved P10 latency (-71.7%) but barely moved P50 and regressed P90 (+2.24%).

## Takeaways
Hierarchical multi-agent design balances specialization with scalability. Letting the LLM route dynamically through reasoning modes beats rigid execution graphs — the overhead of an explicit planning phase can hurt when conditions are uncertain.
