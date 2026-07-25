---
id: cs2228
title: How Rovo Deep Research Works
company: Atlassian
primary_category: genai
sub_category: eval
year: 2025
source_url: https://www.atlassian.com/blog/atlassian-engineering/how-rovo-deep-research-works
tags: [deep-research, rag, rovo, enterprise-search, multi-step-reasoning]
---

# How Rovo Deep Research Works
**Atlassian** · 2025 · [source](https://www.atlassian.com/blog/atlassian-engineering/how-rovo-deep-research-works)

## Problem
Rovo Chat performed well on simple lookup queries ("what's the status of project X?") but fell short on complex requests that require advanced retrieval and synthesis — comparative analysis, multi-source insights, and nuanced questions. Atlassian wanted a feature that could produce detailed research reports over enterprise data within minutes.

## Approach / System design
Deep Research is built as a two-stage RAG framework: query-dependent retrieval with multi-path information gathering, followed by content-grounded answer generation. Complex tasks are decomposed into sub-tasks that run concurrently. Before planning, the system grounds itself in organizational context pulled from Atlassian's Teamwork Graph. Research proceeds iteratively: after each round, the system reflects on findings, identifies knowledge gaps, and plans the next phase. Report generation is structured — an outline is created first, sections are developed in parallel, and everything is synthesized into a cohesive report with inline citations. Internal reasoning is exposed to users for transparency and verifiability.

## Key decisions
- Ground the research plan in the Teamwork Graph's organizational data before decomposing the task.
- Iterative reflect-and-refine loops between research rounds rather than one-shot retrieval.
- Outline-first structured synthesis with independently generated sections merged with inline citations.
- Use reasoning-capable models for planning and reflection, cheaper/faster models for narrower sub-tasks.
- Show reasoning to the user to build trust in the output.

## Stack
Model mix by role: Llama 3.2 8B for query understanding, GPT-4o and GPT-4.1 for sub-agent tasks, Claude 3.7 Sonnet for reasoning, planning, and reflection. Atlassian Teamwork Graph for contextual grounding. Two evaluation frameworks: automated side-by-side comparison (relevance, depth, accuracy, clarity) and reference-free LLM-as-a-judge scoring weighted across five dimensions.

## Results
No explicit quantitative performance metrics are given in the post; quality is tracked through the two evaluation frameworks described above.

## Takeaways
Handling real-world research queries required moving beyond single-pass RAG: structured report generation enables deeper analysis, inline citations provide source attribution, and iterating on observed weaknesses is what makes the system production-worthy.
