---
id: cs2364
title: Applying Large Language Model For Relevance Search In Tencent
company: Tencent
primary_category: search
sub_category: relevance-eval
year: 2025
source_url: https://dl.acm.org/doi/10.1145/3711896.3737193
tags: [llm, relevance-evaluation, knowledge-distillation, bert, hard-negative-mining, web-search]
---

# Applying Large Language Model For Relevance Search In Tencent
**Tencent** · 2025 · [source](https://dl.acm.org/doi/10.1145/3711896.3737193)

## Problem
Relevance identification is central to commercial search engines, which traditionally run encoder-only models like BERT in production. Autoregressive LLMs promise stronger relevance judgment, but two obstacles block direct deployment at web scale: their full ranking capabilities were unexplored, and their computational cost makes real-time serving impractical.

## Approach / System design
Tencent's GenFR work (KDD 2025) has three parts:
1. **Evaluation framework** — systematically assess LLM effectiveness for query-document relevance ranking across four dimensions: ranking objectives, model size, domain-specific pre-training, and prior-knowledge integration, to decide where resources are best spent.
2. **Knowledge distillation** — instead of serving LLMs directly, transfer their ranking capability into the existing BERT-based production relevance models (per the catalog metadata, this includes using LLMs as relevance judges and hard-negative generators for distillation).
3. **Production deployment** — where LLMs do run (in Tencent QQ Browser search), use query-based on-demand computing and quantization to keep costs practical.

## Key decisions
- Measure before deploying: profile what LLM scale, pre-training, and objective actually buy for relevance ranking rather than assuming bigger is better.
- Keep BERT in the hot path and use LLMs offline/asynchronously as teachers, preserving serving latency budgets.
- On-demand computation plus quantization for the LLM components that are deployed online.

## Stack
LLMs as teachers/judges; BERT-family encoder models in the production relevance stack; deployed in Tencent QQ Browser search. Published at KDD 2025 (Proceedings of the 31st ACM SIGKDD Conference, V.2).

## Results
Real-world dataset experiments and online A/B tests showed the approach significantly enhances search engine performance while maintaining operational efficiency; the source abstract states no specific numbers.

## Takeaways
The practical path for LLMs in web search relevance is indirect: evaluate rigorously, distill LLM ranking ability into the cheap encoder models already serving traffic, and reserve online LLM inference for on-demand, quantized use — capability upgrade without a latency or cost regression.
