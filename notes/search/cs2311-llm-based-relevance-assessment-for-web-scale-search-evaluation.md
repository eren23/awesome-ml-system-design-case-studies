---
id: cs2311
title: LLM-based Relevance Assessment for Web-Scale Search Evaluation at Pinterest
company: Pinterest
primary_category: search
sub_category: relevance-eval
year: 2025
source_url: https://arxiv.org/abs/2509.03764
tags: [llm-judge, relevance-assessment, a-b-testing, human-annotation, recsys-2025, arxiv-2025]
---

# LLM-based Relevance Assessment for Web-Scale Search Evaluation at Pinterest
**Pinterest** · 2025 · [source](https://arxiv.org/abs/2509.03764)

## Problem
Evaluating search relevance for online A/B experiments at Pinterest relied on human annotation, whose high cost and long turnaround limit scalability. That bottleneck constrained how many queries could be evaluated, how experiments were sampled, and ultimately how small a quality change an experiment could detect.

## Approach / System design
Pinterest fine-tuned LLMs to act as automated relevance judges for search results, replacing human annotation in the online experimentation loop. Before relying on the automated labels, the team rigorously validated alignment between LLM-generated judgments and human annotations. With annotation cost removed as the constraint, the evaluation system could expand the query set, optimize sampling design, and assess a wider range of search experiences.

## Key decisions
- Fine-tune LLM judges rather than use base models off the shelf.
- Gate adoption on systematic validation against human annotations to establish trust in the automated labels.
- Reinvest the scalability win into experiment sensitivity: larger query sets and better sampling design rather than just cheaper evaluation.

## Stack
Fine-tuned LLMs for relevance judgment integrated into Pinterest's search A/B experimentation pipeline. Specific models and infrastructure are not covered in the source. Presented at the RecSys 2025 EARL workshop.

## Results
The approach significantly reduced the Minimum Detectable Effect (MDE) of online search-quality experiments and produced higher-quality relevance metrics. Specific numeric values are not stated in the source.

## Takeaways
LLM judges change the economics of search evaluation: once validated against human labels, they turn relevance measurement from a scarce resource into an abundant one — and the real payoff is statistical, letting experiments detect smaller effects through bigger, better-designed evaluation sets.
