---
id: cs2219
title: Building DoorDash Assistant: An Engineering Overview
company: DoorDash
primary_category: genai
sub_category: agents
year: 2025
source_url: https://careersatdoordash.com/blog/building-doordash-assistant-an-engineering-overview/
tags: [conversational-ai, multi-agent, customer-support, llm]
---

# Building DoorDash Assistant: An Engineering Overview
**DoorDash** · 2025 · [source](https://careersatdoordash.com/blog/building-doordash-assistant-an-engineering-overview/)

## Problem
DoorDash wanted conversational shopping where a consumer describes what they want and gets reliable recommendations. The hard part is accuracy over constantly changing local-commerce data (menus, prices, inventory, hours, ETAs) that doesn't live in a model's weights, plus personalization that doesn't force users to repeat preferences each session.

## Approach / System design
A four-layer platform: (1) Assistant Runtime — clients, gateway, an orchestrator agent, and domain agents (restaurant discovery, grocery shopping). (2) Managed Agent Services — versioned widget artifacts, session state, consumer memory. (3) a shared MCP tool surface exposing typed business logic and grounding data to all agents. (4) existing DoorDash backend services (search, catalog, cart, order). The orchestrator routes to domain agents over gRPC, with agent pinning maintaining continuity within a session. Every consumer-visible claim must come from a tool call against live system-of-record data on each turn (grounding-first). Memory is three-tier: long-term (daily/weekly batch — dietary preferences, brand affinity), in-session (realtime intent), and agentic (conversation-driven, deduplicated, reconcilable facts). The Assistant proposes but never commits without explicit consumer confirmation.

## Key decisions
- Grounding-first: recompute claims from live data each turn to avoid mismatched availability, pricing, or store status — the largest failure category.
- Multi-agent platform with decoupled domain teams on shared infra so teams iterate without cross-domain regressions.
- Human-in-the-loop: proposals require confirmation; consumers can edit widgets directly or ask for changes conversationally.
- Reversible architecture: model and design choices are easy to roll back, validated via simulation before deploy.

## Stack
Google's Agent Development Kit (ADK), a unified model factory with per-role model selection and provider fallback; Server-Sent Events for streaming, gRPC for agent-to-agent; iOS-first clients with multimodal input (text, image, voice, camera); LLM-as-judge evaluation calibrated to human labels with online/offline alignment and automated failure clustering.

## Results
Operational figures rather than benchmarks: ~7 in 10 messages involve discovery; most consumers who send a first message keep iterating in the same session; a typical grocery turn takes 6–8 LLM calls and low hundreds of thousands of input tokens; end-to-end latency 20–30 seconds; PR volume roughly tripled in the final pre-launch weeks with AI-assisted development.

## Takeaways
Local commerce demands constant grounding. A multi-agent platform with shared evaluation harness lets domain teams iterate quickly, end-to-end session evaluation catches quality unit tests miss, and requiring explicit confirmation before commitment keeps the experience collaborative and builds trust.
