---
id: cs2393
title: "Architecting a trusted agentic platform with graph technologies: A Yahoo case study"
company: Yahoo
primary_category: genai
sub_category: agents
year: 2026
source_url: https://cloud.google.com/blog/products/databases/graph-technologies-underpin-yahoo-system-of-action
tags: [agentic-platform, knowledge-graph, spanner-graph, bigquery-graph, media-buying, governance, a2a-protocol, auditability]
---

# Architecting a trusted agentic platform with graph technologies: A Yahoo case study
**Yahoo** · 2026 · [source](https://cloud.google.com/blog/products/databases/graph-technologies-underpin-yahoo-system-of-action)

## Problem
Digital media buying at Yahoo took weeks of manual coordination across planning, sales, operations, and compliance. Moving to autonomous agents ("system of action" rather than "system of intelligence") raises the core enterprise problem: every autonomous decision must be explainable, policy-compliant, and auditable to regulator standards.

## Approach / System design
A multi-agent Seller Agent platform built on a dual-graph foundation with deliberate separation of duties. The Knowledge Graph (Spanner Graph) grounds decisions in business reality: advertising products, placements, audience segments, inventory, contracts, and governance controls are connected entities, with policies stored as versioned relationships in the graph itself; Gemini embeddings add semantic similarity and graph neural networks infer relationships. The Context Graph (BigQuery Graph) is the auditable memory: operational spans captured via the BigQuery Agent Analytics plugin are shaped into typed decision traces recording every decision point, candidate package, policy evaluation, agent delegation, and execution outcome. Execution flow: a buyer agent submits a campaign brief via the Ad Context Protocol; agents query the knowledge graph for inventory, audiences, contracts, and policies in a single query plan; forecasting models score candidate packages while a governance agent validates consent and brand safety; results auto-approve within policy thresholds or escalate to humans. Delivery and attribution signals are joined back to original decisions for closed-loop learning.

## Key decisions
- Two specialized graphs instead of one: operational truth (Spanner Graph) separated from decision history (BigQuery Graph).
- Policy as versioned graph data rather than logic buried in application code.
- Agents act on deterministic business facts from the graph, not statistical guesses — eliminating hallucination risk in decisions.
- Open protocols (A2A for agent coordination, AdCP for buyer–seller communication) as the auditable common language.
- Auto-approval bounded by policy thresholds, with human escalation beyond them.

## Stack
Spanner Graph (knowledge graph), BigQuery Graph + Agent Analytics plugin/SDK (context graph), GKE (orchestration), Google Agent Development Kit, Agent2Agent (A2A) protocol, Ad Context Protocol (AdCP), Gemini Enterprise Agent Platform (LLM and embeddings).

## Results
Campaign execution went from weeks of manual coordination to seconds, with fully governed live campaigns. Accountability is built in rather than bolted on: "why this package?" is answerable with a single query tracing brief → candidates → scores → policies → outcome.

## Takeaways
- Ground agent decisions in a knowledge graph of business reality; deterministic facts beat probabilistic retrieval for regulated actions.
- Build auditable memory as a first-class system — a queryable context graph turns opacity into explainability and enables closed-loop improvement.
- The durable moat is not the model but the proprietary graph of business operations and its governed decision history, connected through open protocols.
