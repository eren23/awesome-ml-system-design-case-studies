---
id: cs2396
title: How ServiceNow Delivers Production Grade AI Agents
company: ServiceNow
primary_category: genai
sub_category: agents
year: 2025
source_url: https://medium.com/@carolynduby/how-servicenow-delivers-production-grade-ai-agents-f70f51521830
tags: [production-agents, workflow-agents, agentlab, browsergym, agent-evaluation, agent-testing, enterprise]
---

# How ServiceNow Delivers Production Grade AI Agents
**ServiceNow** · 2025 · [source](https://medium.com/@carolynduby/how-servicenow-delivers-production-grade-ai-agents-f70f51521830)

## Problem
Scripted and robotic process automation handle high-volume tasks with repeatable steps, but many enterprise workflows have no regular implementation path. LLM agents can reason over such tasks (e.g., interpret a natural-language request, search the knowledge base, propose or execute a resolution), but getting from proof of concept to a production product that is reliable, safe, scalable, and cost-effective is the hard part. This article distills how ServiceNow researchers (Nicolas Chapados and Alexandre Drouin, presenting in the Berkeley LLM Agents MOOC) approach that gap.

## Approach / System design
ServiceNow splits workflow agents into two categories. API Agents call well-defined programming interfaces: more efficient and lower risk, but only where APIs exist. Web Agents navigate web pages: universally applicable but less efficient, more brittle, and higher risk. For the full agent lifecycle, ServiceNow open-sourced the TapeAgents framework: low-code development where everything the agent does and observes is recorded to a consistent log format (the "tape"), so sessions can be replayed for debugging and auditing, and an optimizer can mine tapes from many runs to fine-tune smaller models that match performance at lower cost. For web-agent research, two more open-source frameworks: BrowserGym unifies multiple benchmarks in one format, and AgentLab develops and evaluates agents against them; the WorkArena benchmark measures agents on realistic ServiceNow IT service-management tasks by specifying the required end state rather than the path.

## Key decisions
- Prefer API agents over web agents wherever APIs exist — efficiency and risk both favor structured interfaces.
- Record every agent step and observation as replayable tapes, making debugging, auditing, and optimization first-class rather than afterthoughts.
- Use tape corpora to distill/fine-tune cheaper models with equal performance.
- Evaluate agents with the GReADTH criteria: Grounded, Responsive, Accurate, Disciplined, Transparent, Helpful.
- Benchmark on end-state-defined real-world tasks (WorkArena), allowing multiple valid solution paths.

## Stack
Open-source frameworks: TapeAgents (lifecycle, logging, optimization), AgentLab (agent development and evaluation), BrowserGym (unified benchmark environments), WorkArena (real-world task benchmark on the ServiceNow platform).

## Results
The frameworks are released and in use for agent research and development. ServiceNow's own assessment is that web agents are not production-ready: even the best fall well short of human performance on realistic web tasks — planners see only the current page, pages demand long context windows and multimodal understanding, agents hallucinate non-working solutions, and prompt injection via page content or form fields is a live safety risk. No quantitative benchmark numbers are given in the source.

## Takeaways
- Production-grade agents need lifecycle tooling — recorded, replayable execution traces — not just a good prompt.
- The API-vs-web agent split is a useful risk/efficiency frontier: constrain agents to structured interfaces when possible.
- Honest evaluation on realistic benchmarks tempers hype: web agents remain a research frontier while API-based workflow agents are the nearer-term production path.
