---
id: cs2275
title: Cost-Effective E-Commerce Catalog Translation at Scale Ensuring Named Entity Protection
company: Walmart
primary_category: nlp
sub_category: translation
year: 2025
source_url: https://aclanthology.org/2025.emnlp-industry.81/
tags: [machine-translation, catalog-translation, named-entity-protection, cost-reduction, e-commerce, emnlp, multilingual, spanish, french]
---

# Cost-Effective E-Commerce Catalog Translation at Scale Ensuring Named Entity Protection
**Walmart** · 2025 · [source](https://aclanthology.org/2025.emnlp-industry.81/)

## Problem
Translating a huge e-commerce catalog (English to Spanish and French) must be cheap at scale while never corrupting named entities — brand names, SKUs, and similar tokens must survive translation untouched. General-purpose LLMs can translate but are costly and don't guarantee entity preservation.

## Approach / System design
Walmart's Translation Platform runs two pipeline types: daily batch pipelines for bulk catalog updates and real-time API pipelines for immediate translation needs. Serving uses GPU-accelerated inference servers for optimized T5-based translation models, with CPU nodes handling supporting processing. A Reference Generator component enforces named-entity protection, and a linguist-driven rule engine provides explainable quality evaluation combining BLEU, COMET, and custom e-commerce-specific metrics. A version-tracking system supports robust enterprise rollouts.

## Key decisions
- Purpose-built, optimized T5-based models instead of general-purpose LLMs, trading generality for 10x-100x cost savings.
- A dedicated Reference Generator to guarantee >99% preservation of non-translatable entities rather than trusting the model.
- Human-in-the-loop quality: linguist-authored rules plus automatic metrics (BLEU, COMET, custom) for explainable evaluation.
- Split batch and real-time paths so bulk updates and interactive needs each get an appropriate pipeline.

## Stack
Optimized T5-based neural MT models on GPU inference servers; CPU processing nodes; Reference Generator for entity protection; linguist rule engine with BLEU/COMET/custom metrics; version-tracking for rollouts. Published at EMNLP 2025 Industry Track.

## Results
- Millions of listings translated per day with sub-second latency.
- 10x-100x cost savings versus general-purpose LLMs.
- >99% preservation of non-translatable named entities.
- In production for English→Spanish and English→French.

## Takeaways
Specialized MT with explicit entity-protection machinery beats general LLMs on both cost and correctness for catalog translation. Guaranteeing domain constraints (SKU/brand preservation) via a dedicated system component is more reliable than prompting a general model, and explainable linguist-driven evaluation is what makes enterprise rollout defensible.
