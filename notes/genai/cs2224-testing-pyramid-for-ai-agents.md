---
id: cs2224
title: Testing Pyramid for AI Agents
company: Block
primary_category: genai
sub_category: agents
year: 2026
source_url: https://engineering.block.xyz/blog/testing-pyramid-for-ai-agents
tags: [agent-testing, evaluation, testing-pyramid, llm-agents]
---

# Testing Pyramid for AI Agents
**Block** · 2026 · [source](https://engineering.block.xyz/blog/testing-pyramid-for-ai-agents)

## Problem
The classic testing pyramid (unit → integration → UI) assumes determinism: same input, same output. LLM agents break that assumption immediately, which leads to flaky tests or teams abandoning testing altogether.

## Approach / System design
Block reframes the pyramid as layers of increasing uncertainty tolerance rather than test types. Base layer (deterministic foundations): mock LLM providers return canned responses so unit tests can cover retry logic, tool schemas, and delegation — answering "did we write correct software?". Middle layer (reproducible reality): record real MCP servers and LLMs once, then replay them, validating tool-call sequences and interaction flow instead of exact output. Upper layer (probabilistic performance): structured benchmarks run many times, measuring success rate over runs — a single run tells you almost nothing, patterns tell you everything. Top layer (vibes and judgment): LLM-as-judge with explicit rubrics, three runs and majority voting. Plus first-person smoke tests where the agent validates its own capabilities end-to-end.

## Key decisions
- Mock LLM providers in unit tests for speed and cost.
- Record/replay external tool interactions rather than hitting them live in CI.
- Avoid live LLM calls in CI — too expensive and flaky.
- Measure trends across runs instead of single pass/fail outcomes.
- Formalize subjective quality with rubric-based LLM-as-judge and majority voting rather than ignoring it.

## Stack
MCP servers for external tools, generic LLM providers, JSON fixture files for recorded test data; code examples in Rust.

## Results
No quantitative results are stated in the post.

## Takeaways
Agent testing has to accept probabilistic outcomes. Deterministic foundations still matter at the base, but higher layers must shift from pass/fail toward trend analysis and explicit evaluation frameworks.
