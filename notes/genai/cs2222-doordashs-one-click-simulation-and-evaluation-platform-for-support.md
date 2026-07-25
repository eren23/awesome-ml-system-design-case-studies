---
id: cs2222
title: DoorDash's One-Click Simulation and Evaluation Platform for Support Chatbots
company: DoorDash
primary_category: genai
sub_category: chatbots
year: 2025
source_url: https://careersatdoordash.com/blog/doordashs-one-click-simulation-and-evaluation-platform-for-support-chatbots/
tags: [simulation, evaluation-platform, chatbot, customer-support, llm]
---

# DoorDash's One-Click Simulation and Evaluation Platform for Support Chatbots
**DoorDash** · 2025 · [source](https://careersatdoordash.com/blog/doordashs-one-click-simulation-and-evaluation-platform-for-support-chatbots/)

## Problem
Validating support-chatbot changes was slow: the legacy approach used 1% production traffic rollouts with manual transcript review, taking weeks to months and leaving blind spots for edge cases, policy violations, and regressions from prompt or infrastructure changes.

## Approach / System design
A closed-loop platform with four components. (1) Scenario generation pipeline: LLM extraction turns production support transcripts into structured, replayable test cases (customer stories, behavioral patterns, issue types). (2) LLM simulator: acts as a realistic customer with dynamic, context-aware prompts driving multi-turn conversations, keeping state across turns and supporting free-form and scripted modes. (3) Mock server: intercepts chatbot tool calls and routes simulation traffic to mock services using production-backed data modified per scenario, giving realism plus determinism. (4) Evaluation service: LLM-as-judge scoring with feature-specific rubrics (escalation decisions, policy compliance, tone) producing binary pass/fail metrics.

## Key decisions
- White-box end-to-end testing that simulates whole conversation loops including tool interactions and context retrieval, not just message exchanges.
- Ground scenarios in real transcripts and APIs to preserve realistic user behavior.
- Mock-aware routing: the chatbot distinguishes simulation from production via routing headers, isolating traffic without changing logic.
- Feature-specific rubrics rather than a generic standard.

## Stack
LLM-based customer simulation; gRPC and Model Context Protocol (MCP) for tool mocking; SQL-backed persistence for historical comparison and trend monitoring; multi-turn conversation state management.

## Results
Validation trial vs. production (1% traffic): simulation ran 302 conversations in 5 minutes at a 46% escalation rate, versus production's 175 conversations in 7 hours at 44% — matching production-like behavior. Hallucinations in simulations were reduced 90% through platform improvements.

## Takeaways
Shifting validation left turned hours of waiting on live traffic into minutes of automated testing. The simulation-evaluation flywheel lets teams run dozens of prompt experiments before any customer exposure while keeping production-quality confidence and reducing launch risk.
