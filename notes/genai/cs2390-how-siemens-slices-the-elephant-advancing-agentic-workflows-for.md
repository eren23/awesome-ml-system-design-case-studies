---
id: cs2390
title: "How Siemens 'Slices the Elephant,' Advancing Agentic Workflows for Industrial Software Development"
company: Siemens
primary_category: genai
sub_category: agents
year: 2026
source_url: https://cloud.google.com/blog/products/ai-machine-learning/how-siemens-sliced-the-elephant-modernizing-legacy-code-with-agentic-workflows
tags: [code-modernization, legacy-code, multi-agent, knowledge-graph, spanner-graph, agentic-workflows, gemini]
---

# How Siemens 'Slices the Elephant,' Advancing Agentic Workflows for Industrial Software Development
**Siemens** · 2026 · [source](https://cloud.google.com/blog/products/ai-machine-learning/how-siemens-sliced-the-elephant-modernizing-legacy-code-with-agentic-workflows)

## Problem
Siemens must modernize hundreds of millions of lines of legacy code, built over more than a decade, powering factory automation, energy, and transportation systems. Codebases exceed any LLM context window; knowledge is fragmented across code, Jira, Confluence, and scanned PDFs from the 2000s; tracing code to decade-old requirements is impractical manually; and because these systems run 15–20 years under strict compliance, hallucinated code is operationally unacceptable.

## Approach / System design
A domain-aware "Knowledge Fabric" models the codebase and its documentation as a graph rather than flat text: Spanner Graph stores structural relationships (class → file → module) queried via GQL, Spanner ANN provides semantic embedding search across the codebase, and Spanner full-text search gives precise node/edge lookup — the three fused for retrieval. All knowledge sources (PDFs, Jira, Confluence) are mapped into the same graph. On top sits an agentic workflow ("slicing the elephant") of specialized agents: a Search Agent explores the code graph and cross-references docs; a User Story Agent produces context-linked requirements and acceptance criteria; an Architecture Impact Agent predicts side effects before any code changes; a Task Breakdown Agent decomposes work into small, context-rich tasks; and a Coding Agent implements them. A human stays in the loop at every step.

## Key decisions
- Rejected generic RAG: code has inherent structure, so a graph-native design preserves relationships that flat vector stores lose.
- Multi-search fusion (GQL structural + embeddings + full-text) for precise, grounded retrieval.
- Decompose refactoring so each agent task is small and unambiguous enough to succeed — the coding agent only works after upstream analysis agents have done theirs.
- Explainability as a mandate: every AI output must be traceable and verifiable, reflecting industrial safety requirements.

## Stack
Spanner Graph + GQL, Spanner ANN vector search, Spanner full-text search; Google Agent Development Kit (ADK) for orchestration; Gemini API / Enterprise Agent Platform as LLM backbone; Anthropic Claude Code for code generation.

## Results
Dependency analysis that took senior engineers several days now takes far less time via the Knowledge Fabric (the post cites minutes-scale exploration). A pilot migrating legacy control panels to web interfaces reduced overall coding effort while preserving system integrity, shifting engineers from repetitive tracing work toward customer-facing value. Specific productivity metrics are not quantified in the source.

## Takeaways
- Legacy modernization at industrial scale needs domain-aware structure (knowledge graphs), not generic RAG.
- "Slicing the elephant" is the core pattern: large ambiguous tasks fail; small, well-scoped, context-rich agent tasks succeed.
- A unified graph turns fragmented artifacts (code, tickets, PDFs) into queryable context, and graph-grounded retrieval plus human review keeps outputs verifiable for safety-critical software.
