---
id: cs2394
title: "Stop Stuffing Prompts: How Asana Made Agents More Effective Through Context Engineering"
company: Asana
primary_category: genai
sub_category: agents
year: 2025
source_url: https://asana.com/inside-asana/context-engineering
tags: [context-engineering, rag, ai-agents, ai-studio, context-window, intent-filtering]
---

# Stop Stuffing Prompts: How Asana Made Agents More Effective Through Context Engineering
**Asana** · 2025 · [source](https://asana.com/inside-asana/context-engineering)

## Problem
Standard "retrieve and stuff" RAG degrades as data volume grows: irrelevant content buries the relevant, model performance drops, latency and cost balloon, and vector similarity alone ignores what the user actually intends. Asana needed its AI Studio agents to work over large workspaces without drowning the context window.

## Approach / System design
Intent-augmented retrieval: analyze the query's intent up front and let it drive what gets loaded, in two phases. (1) Filter first — translate the natural-language query into structured filters (fields, time ranges, data sources, scope, dates, completion status, field-level specificity, evaluated in parallel) so irrelevant data is eliminated at the source before any fetch. (2) Sort and summarize — rerank results with cross-encoders that consider both query and content rather than plain vector similarity, order results so the most relevant come first (LLMs attend more to early context), and summarize long content with the user's question in mind rather than generic truncation.

## Key decisions
- Put user intent, not similarity scores, at the center of retrieval.
- Filter before fetching instead of fetching then pruning.
- Cross-encoder reranking over raw vector similarity.
- Intent-conditioned summarization instead of blind truncation of long documents.

## Stack
Asana AI Studio's agent platform with a retrieval layer of structured filter generation, cross-encoder rerankers, and query-conditioned summarizers over Asana workspace data. Specific model/vendor details are not covered in the source.

## Results
Measured in production testing: 35% reduction in total input tokens (field filtering alone contributed ~40% token savings), 24% faster p95 response times, 30% lower cost per call, and assertion accuracy improved from 92–94% to 95–96%.

## Takeaways
- Less context, chosen well, beats more context: trimming input tokens improved accuracy while cutting cost and latency.
- Intent analysis is the highest-leverage step in the retrieval pipeline — it makes every downstream stage cheaper and sharper.
- Ordering matters: placing the most relevant content first exploits how LLMs allocate attention.
