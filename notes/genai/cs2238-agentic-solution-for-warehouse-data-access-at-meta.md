---
id: cs2238
title: Agentic Solution for Warehouse Data Access at Meta
company: Meta
primary_category: genai
sub_category: agents
year: 2025
source_url: https://engineering.fb.com/2025/08/13/data-infrastructure/agentic-solution-for-warehouse-data-access/
tags: [data-warehouse, text-to-sql, agents, data-access, nl-interface]
---

# Agentic Solution for Warehouse Data Access at Meta
**Meta** · 2025 · [source](https://engineering.fb.com/2025/08/13/data-infrastructure/agentic-solution-for-warehouse-data-access/)

## Problem
As Meta's data warehouse grew, managing access and security became increasingly complex. Traditional hierarchical, role-based access control could not cope with the cross-domain access patterns that AI systems introduced, and the manual approval workflow for data access consumed significant engineer and owner time while security risk kept multiplying.

## Approach / System design
Meta built a multi-agent architecture split along the two sides of an access request. Data-user agents comprise three specialized sub-agents: one that suggests alternatives when access to data is restricted, one that enables low-risk exploration through context-aware access, and one that negotiates permission requests with data owners. Data-owner agents handle security operations by following documented SOPs and proactively configure access rules. To make the warehouse legible to LLMs, it was reimagined as textual resources organized in hierarchical folders, since LLMs communicate through text. Context management operates in three modes: automatic (triggered by blocked-access scenarios), static (an explicit user-defined scope), and dynamic (metadata- and similarity-based filtering).

## Key decisions
- Intention management that captures both explicit intentions (role-based) and implicit ones inferred from user activity across diffs, tasks, posts, incidents, dashboards, and documents.
- Guardrails including rule-based risk assessment, query-level access control, and daily-refreshing data-access budgets.
- Human-in-the-loop oversight retained during the negotiation phase between user and owner agents.
- Transparency via comprehensive logging and audit trails for every agent decision.

## Stack
LLMs for reasoning about context-specific business needs; query analyzers for query-shape analysis (aggregation and sampling detection); internal activity-tracking tools; metadata systems storing table summaries and column descriptions.

## Results
No quantitative metrics are given in the post; Meta describes its evaluation methodology (daily evaluation and feedback loops) without publishing numbers.

## Takeaways
LLMs make it possible to reason about nuanced, context-specific business needs that were previously hard to model analytically. Agent-to-agent collaboration and tool evolution remain open challenges beyond human-agent interaction, and daily evaluation with feedback loops is essential for catching regressions and improving accuracy.
