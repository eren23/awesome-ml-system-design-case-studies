---
id: cs2276
title: Weaving Together Review Insights by Leveraging LLMs
company: Best Buy
primary_category: nlp
sub_category: summarization
year: 2025
source_url: https://aclanthology.org/2025.naacl-industry.36/
tags: [review-summarization, product-reviews, llm, feature-extraction, naacl, opinion-mining, e-commerce]
---

# Weaving Together Review Insights by Leveraging LLMs
**Best Buy** · 2025 · [source](https://aclanthology.org/2025.naacl-industry.36/)

## Problem
The volume of customer reviews in online retail creates information overload: shoppers can't realistically read through the continuous stream of feedback on a product, making it hard to extract the signal needed for purchase decisions.

## Approach / System design
RevieWeaver, a framework that automatically extracts key product features from customer reviews and weaves them into concise product summaries. It combines LLM-based processing with semantic similarity analysis to identify and group features across reviews, then generates summaries designed to be unbiased and faithful to the underlying review content.

## Key decisions
- Pair LLMs with semantic similarity matching for feature extraction and grouping rather than relying on free-form LLM generation alone.
- Design for reproducibility and controllability of outputs — important for consumer-facing summaries that must accurately reflect input reviews.
- Engineer the pipeline for scale-out over the full review corpus rather than per-request summarization.

## Stack
LLMs for feature extraction and summary generation, combined with semantic similarity analysis for grouping. Specific models not disclosed in the abstract. Published at NAACL 2025 Industry Track (with Microsoft).

## Results
The system scales efficiently to 30 million product reviews in production. The paper reports that the generated assessments are unbiased and reliably reflect the input reviews; no further quantitative metrics are given in the abstract.

## Takeaways
Review summarization at retail scale is as much a systems problem as a modeling one: semantic grouping plus controlled LLM generation keeps summaries faithful and reproducible while processing tens of millions of reviews. Surfacing aggregated feature-level insights turns raw review volume from a liability into a decision aid.
