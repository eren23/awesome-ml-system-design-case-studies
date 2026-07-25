---
id: cs2310
title: "LEAPS: An LLM-Empowered Adaptive Plugin in Taobao AI Search"
company: Taobao
primary_category: search
sub_category: relevance-eval
year: 2026
source_url: https://arxiv.org/abs/2601.05513
tags: [llm, query-expansion, relevance-verification, conversational-search, broaden-and-refine, arxiv-2026]
---

# LEAPS: An LLM-Empowered Adaptive Plugin in Taobao AI Search
**Taobao** · 2026 · [source](https://arxiv.org/abs/2601.05513)

## Problem
Taobao users increasingly type natural-language, multi-constraint queries instead of keywords, and the traditional e-commerce stack faces a dilemma: honoring a precise natural-language query often yields zero results, while simplifying the query floods users with noisy results that impair purchase decisions.

## Approach / System design
LEAPS is a "Broaden-and-Refine" plugin pair wrapped around the existing retrieval stack. Upstream, an LLM Query Expander broadens recall by generating adaptive, complementary query combinations to grow the candidate pool. Downstream, an LLM Relevance Verifier refines results by filtering noise, synthesizing multi-source signals — including OCR text from images and product reviews — with chain-of-thought reasoning to keep only genuinely relevant items. The plugin design is non-intrusive: it preserves the existing short-text retrieval path and integrates cheaply with diverse back-ends. It has been fully deployed in Taobao AI Search since August 2025, serving hundreds of millions of users monthly.

## Key decisions
- Split the problem into broaden (query expansion for recall) and refine (relevance verification for precision) rather than trying to fix retrieval itself.
- Train the Query Expander in three stages: inverse data augmentation, posterior-knowledge supervised fine-tuning, and diversity-aware reinforcement learning.
- Give the Relevance Verifier multi-source evidence (OCR text, reviews) plus chain-of-thought reasoning to disambiguate difficult results.
- Ship as a non-intrusive plugin so the mature keyword-search path is untouched and back-end integration stays low-cost.

## Stack
LLM-based Query Expander (inverse data augmentation → posterior-knowledge SFT → diversity-aware RL) and LLM Relevance Verifier (multi-signal, chain-of-thought), deployed as plugins around Taobao's existing retrieval back-ends. Model specifics are not covered in the source.

## Results
Fully deployed in production since August 2025, serving hundreds of millions of monthly users. Specific numeric metrics are not stated in the source.

## Takeaways
For conversational commerce queries, wrapping a proven retrieval stack with LLM plugins at both ends — expansion before, verification after — resolves the zero-results-vs-noise dilemma without rebuilding search. Non-intrusive integration was key to deploying LLM capability at Taobao scale quickly.
