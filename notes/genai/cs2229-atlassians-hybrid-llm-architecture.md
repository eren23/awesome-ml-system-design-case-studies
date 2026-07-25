---
id: cs2229
title: Atlassian's Hybrid LLM Architecture
company: Atlassian
primary_category: genai
sub_category: llm
year: 2025
source_url: https://www.atlassian.com/blog/atlassian-engineering/hybrid-llm
tags: [hybrid-llm, model-routing, cost-optimization, rovo, llm-architecture]
---

# Atlassian's Hybrid LLM Architecture
**Atlassian** · 2025 · [source](https://www.atlassian.com/blog/atlassian-engineering/hybrid-llm)

## Problem
Rovo Chat lets enterprise users query workplace data scattered across many platforms via natural language. It must handle open-domain enterprise Q&A over enterprise search, help users consume content efficiently, and assist with content creation — and doing every step with a large frontier model would be needlessly slow and expensive.

## Approach / System design
A four-stage pipeline with a right-sized model per task. (1) Query rewriting: a two-step process producing a semantic query (coreference resolution, context injection — e.g., "can I bring a dog to the office" generalizes to "office pet policy") plus multiple keyword queries, with complex questions decomposed into simpler ones. (2) Plugin routing: BERT-based binary classifiers for high-frequency intents route across five primary plugins (Search-QA, Content-Read, Jira-JQL, People, Page-Search), searching sources like Jira, Confluence, Google Docs, SharePoint, and Slack in parallel. (3) Plugin helpfulness verification: small language models validate that retrieved content is actually relevant before generation. (4) Response generation: a full-size LLM produces the answer, with automatic prompt tuning.

## Key decisions
- Route each pipeline stage to the smallest model that holds quality: for query rewriting, LLaMA-3 8B performed on par with heavy LLMs while being cheaper and faster.
- Evaluate with LLM judges over an internal 241-query evaluation set instead of traditional metrics, after establishing 79-95% agreement with human annotators.
- Stay model-agnostic — GPT, Claude, Gemini, Mistral, and LLaMA were all tested — and retest regularly as the field moves.

## Stack
Mix of frontier LLMs (GPT, Claude, Gemini, Mistral) and open models (LLaMA-3 8B), BERT classifiers for routing, SLMs for verification, Atlassian's proprietary Teamwork Graph, and connectors to Jira, Confluence, Atlas, Google Docs, SharePoint, and Slack.

## Results
Query optimization added +10% answer precision while cutting latency 17%. Plugin-routing accuracy ranged 73.1-94.2%, helpfulness verification 88-98.9%, response generation 81.3-93.7%, and LLM-judge agreement with humans 79-95%.

## Takeaways
A hybrid model portfolio is pragmatism over purity: small models suffice for low-complexity stages, meaningfully cutting cost and latency. Manual inspection of internal dogfooding data — reading through hundreds of rewritten queries — proved the most useful evaluation activity, and reference-based human-in-the-loop judgment matters in enterprise contexts where generic answers miss organizational nuance.
