---
id: cs2226
title: Agent Guardrails and Controls
company: Block
primary_category: genai
sub_category: agents
year: 2026
source_url: https://engineering.block.xyz/blog/agent-guardrails-and-controls
tags: [guardrails, agent-safety, llm-safety, controls, fintech]
---

# Agent Guardrails and Controls
**Block** · 2026 · [source](https://engineering.block.xyz/blog/agent-guardrails-and-controls)

## Problem
Content injection attacks against LLM agents: malicious text embedded in tool responses can manipulate the model into executing unauthorized actions, because agents have no reliable way to distinguish data from instructions inside the context window.

## Approach / System design
Block adapts the browser-security CORS model to agentic systems, mapping the LLM to untrusted client-side code, the agent to the browser, and MCP to the web server. The agent tracks the provenance of tool-call requests: a tool call requested after a tool response (a non-user actor) rather than a direct human prompt is treated as "cross-origin" and hits a stop-gate requiring explicit human approval. Additionally, all tool-call responses are flushed from the context window between user turns, so stale tool output can't carry injected instructions into later turns.

## Key decisions
- Tool-call origin validation: block tool executions requested downstream of tool responses unless a human approves, mirroring CSRF defenses.
- Context window flushing between user turns to defeat inter-turn injection via old tool outputs.
- Deterministic enforcement: authorization decisions live entirely in the agent's code, never delegated to the LLM.

## Stack
Model Context Protocol (MCP); Prompt Guard referenced as a classifier-based injection-detection approach; Meta's Agent Rule of Two cited as a related security principle. A proof of concept and benchmarking effort for goose was in progress at publication.

## Results
No benchmark numbers yet — the goose proof of concept and benchmarking were still in progress when the post was published.

## Takeaways
Content injection in agents mirrors CSRF in browsers, so browser-era defenses translate. Dropping tool responses between turns raises attack difficulty substantially while keeping the agent useful. The scheme trusts the agent codebase itself and doesn't stop everything: second-order injections, deliberate operator misuse, and attacks on non-tool outputs remain open problems.
