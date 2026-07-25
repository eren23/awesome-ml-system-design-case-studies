---
id: cs2277
title: Rationale-Guided Distillation for E-Commerce Relevance Classification: Bridging Large Language Models and Lightweight Cross-Encoders
company: Amazon
primary_category: nlp
sub_category: classification
year: 2025
source_url: https://aclanthology.org/2025.coling-industry.12/
tags: [knowledge-distillation, relevance-classification, e-commerce, cross-encoder, bert, llm, coling, query-product-matching]
---

# Rationale-Guided Distillation for E-Commerce Relevance Classification: Bridging Large Language Models and Lightweight Cross-Encoders
**Amazon** · 2025 · [source](https://aclanthology.org/2025.coling-industry.12/)

## Problem
Query-product relevance classification is critical for e-commerce search — showing irrelevant products hurts user experience and engagement. LLMs classify relevance well but are too expensive and slow for production-scale inference, while small cross-encoders that fit the latency budget lag in accuracy.

## Approach / System design
Rationale-guided knowledge distillation: a 7B-parameter teacher LLM generates both relevance labels and natural-language rationales explaining each decision. These rationales are used as an additional training signal when distilling into a 110M-parameter BERT-based cross-encoder student. The rationales transfer the teacher's reasoning, not just its labels, so the student captures decision logic without needing the LLM at inference time.

## Key decisions
- Distill rationales (explanations of why a query-product pair is relevant), not just hard labels — the reasoning signal is what closes the teacher-student gap.
- Keep the production model a standard 110M cross-encoder so inference stays cheap and deployment-compatible.
- Evaluate across multilingual e-commerce datasets, ESCI, and GLUE to validate generality.

## Stack
7B LLM teacher generating labels + rationales; 110M BERT-based cross-encoder student for production inference. Published at COLING 2025 Industry Track.

## Results
- +1.4% ROC-AUC over baseline cross-encoders on 9 multilingual e-commerce datasets, +2.4% on 3 ESCI datasets, +6% on GLUE.
- Student matches the 7B teacher within <1% ROC-AUC.
- ~50x faster inference per sample than the teacher LLM.

## Takeaways
LLM rationales are an effective distillation medium: they let a model ~60x smaller reach near-teacher accuracy. For latency-bound tasks like search relevance, distilling reasoning into a small cross-encoder gets LLM-quality classification at production cost, avoiding any LLM in the serving path.
