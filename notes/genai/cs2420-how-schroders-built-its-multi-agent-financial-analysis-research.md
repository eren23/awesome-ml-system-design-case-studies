---
id: cs2420
title: "How Schroders Built Its Multi-Agent Financial Analysis Research Assistant"
company: Schroders
primary_category: genai
sub_category: agents
year: 2025
source_url: https://cloud.google.com/blog/topics/customers/how-schroders-built-its-multi-agent-financial-analysis-research-assistant
tags: [multi-agent, financial-analysis, vertex-ai, langgraph, research-assistant]
---

# How Schroders Built Its Multi-Agent Financial Analysis Research Assistant
**Schroders** · 2025 · [source](https://cloud.google.com/blog/topics/customers/how-schroders-built-its-multi-agent-financial-analysis-research-assistant)

## Problem
Financial analysts at Schroders typically cover 20–30 companies in depth, and initial research reports could take days to complete because the majority of that time was spent on data collection rather than analysis. The goal was to shift analyst effort toward higher-value strategic thinking by automating the research gathering phase.

## Approach / System design
Schroders built a multi-agent research assistant on Vertex AI using LangGraph for orchestration. A Router Agent classifies user intent and delegates to specialized agents—including an R&D Analysis Agent, a Working Capital Agent, and a Porter's 5 Forces Agent that itself spawns child agents in parallel for sub-tasks. Agents access three data layers: internal documents via Vertex AI Search, structured financial data via BigQuery (with natural language to SQL translation), and public market data via Google Search. LangGraph manages state, cyclical workflows, and human-in-the-loop checkpoints between agents.

## Key decisions
The team initially built on native Vertex AI Agent Builder function calling but migrated to LangGraph to gain native state management, support for cyclical workflows, and cleaner parent-child agent hierarchies—accepting more framework overhead in exchange for significantly reduced custom complexity. Each agent is intentionally scoped to fewer than five tools to improve reliability and reduce the chance of tool misuse. A templated system prompt architecture separates developer-controlled generalization from analyst-controlled business logic, giving analysts control over domain-specific behavior without requiring code changes.

## Stack
Vertex AI Agent Builder, Gemini foundation models, LangGraph, BigQuery, Vertex AI Search, Firestore (configuration versioning and conversation history), Google Search, Cloud Logging, Cloud Monitoring, Vertex AI Generative AI Evaluation.

## Results
The prototype demonstrated that detailed company research analysis could be reduced from days to minutes. Evaluation uses a combination of automated metrics (task success rate, tool accuracy, latency) and human-in-the-loop analyst review scored against a ground truth dataset built from structured analyst feedback.

## Takeaways
Limiting each agent to a small, focused toolset and decomposing complex financial workflows into the smallest logical atomic units produced more reliable outputs than attempting to handle broad research tasks with a single generalist agent. Investing in a structured evaluation framework anchored to analyst feedback—rather than relying on generic LLM benchmarks—was essential for building the trust needed for adoption in a high-stakes investment management context.
