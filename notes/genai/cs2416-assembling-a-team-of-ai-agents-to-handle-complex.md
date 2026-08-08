---
id: cs2416
title: "Assembling a Team of AI Agents to Handle Complex Mortgage Questions at Mr. Cooper"
company: Mr. Cooper
primary_category: genai
sub_category: agents
year: 2025
source_url: https://cloud.google.com/blog/topics/financial-services/assembling-a-team-of-ai-agents-to-handle-complex-mortgage-questions-at-mr-cooper
tags: [multi-agent, mortgage, customer-support, vertex-ai, agent-builder, ciera]
---

# Assembling a Team of AI Agents to Handle Complex Mortgage Questions at Mr. Cooper
**Mr. Cooper** · 2025 · [source](https://cloud.google.com/blog/topics/financial-services/assembling-a-team-of-ai-agents-to-handle-complex-mortgage-questions-at-mr-cooper)

## Problem
Mortgage servicing involves complex, cross-document queries—customers ask questions that require simultaneously interpreting loan documents, escrow analyses, and regulatory information. Legacy keyword-based automation fails when conversation turns are unexpected, leaving human agents to perform tedious research rather than focusing on customer relationships.

## Approach / System design
Mr. Cooper deployed CIERA (Coaching Intelligent Education & Resource Agent), a multi-agent system with clearly separated roles: Ava orchestrates task decomposition and agent delegation; Lex agents handle complex analysis such as escrow calculations and loan application review; Sky navigates internal knowledge bases; Remy maintains memory and personalizes workflows; Iris validates outputs and detects hallucinations using Model Armor; and Sage monitors all agents and optimizes orchestration over time. Parallel execution is used where tasks are independent. Human agents review AI-synthesized results at a validation checkpoint before final delivery, keeping humans central to decision-making.

## Key decisions
Specialization was favored over a single generalist agent because each mortgage task type—calculations, document lookup, memory—benefits from a focused toolset and targeted prompting. An evaluation framework called Agentic Pulse tracks faithfulness, relevance, and safety metrics in real time, correlating them with business KPIs such as average handle time and customer satisfaction. A sandboxed human-in-the-loop testing environment allows continuous refinement before changes reach production.

## Stack
Vertex AI, Vertex AI Agent Builder, Agent Development Kit (ADK), Model Context Protocol (MCP), Model Armor (hallucination detection and grounding), Agentic Pulse monitoring dashboard.

## Results
Specific metrics are projected rather than reported: expected improvements in average handling time reduction, first-contact resolution rates, and customer satisfaction scores. The source does not provide production numbers at the time of publication.

## Takeaways
Mirroring successful human team structures—with distinct roles for orchestration, analysis, memory, and quality control—produces more reliable multi-agent systems than monolithic designs, especially in regulated industries where errors carry significant consequences. In mortgage servicing, governance mechanisms (hallucination detection, faithfulness scoring, human review checkpoints) are not optional additions but foundational requirements for deployment.
