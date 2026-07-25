---
id: cs2314
title: "Unified Multi-Task Relevance Modeling for E-Commerce: Comparing Task Routing Architectures Across LLMs and Cross-Encoders"
company: Walmart
primary_category: search
sub_category: relevance-eval
year: 2026
source_url: https://arxiv.org/abs/2606.23919
tags: [multi-task-learning, relevance-modeling, cross-encoder, llm, e-commerce, task-routing, arxiv-2026]
---

# Unified Multi-Task Relevance Modeling for E-Commerce: Comparing Task Routing Architectures Across LLMs and Cross-Encoders
**Walmart** · 2026 · [source](https://arxiv.org/abs/2606.23919)

## Problem
Walmart's e-commerce stack needs relevance judgments for six different entity-pair types (query-product, query-query, product-product, and others). Running a separate model per task is expensive, and the tasks have different data volumes, different semantic requirements, and potentially conflicting learning signals — so naive joint training risks interference while single-task models forgo knowledge transfer.

## Approach / System design
Train one unified model over all six entity-pair tasks with a shared three-point relevance scale, and systematically compare three task-routing architectures: text prefix routing (task identity in the input text), multi-head classification (per-task output heads), and multi-head with private transformer layers (MHP). The comparison spans two model families — LoRA-adapted decoder-only LLMs and fully fine-tuned cross-encoders. A majority-vote ensemble exploits the prediction diversity that private-layer routing induces.

## Key decisions
- Standardize all six tasks onto a shared three-point relevance scale so they can be trained jointly.
- Treat task routing as the central design variable and evaluate it symmetrically across LLM and cross-encoder architectures.
- Give tasks private transformer layers on top of shared representations (MHP) to contain cross-task interference, then ensemble across the resulting diversity.

## Stack
LoRA-adapted decoder-only LLMs and fully fine-tuned cross-encoder models; evaluation on a 453K-example test set. Specific base models are not covered in the source.

## Results
The MHP ensemble reached 89.96% accuracy on the 453K test examples. Multi-task training delivered up to 14% improvement on low-resource tasks versus single-task baselines. A notable asymmetry: removing text prefixes (without private layers) severely degraded decoder-only LLMs but not cross-encoders, showing encoders and decoders encode task identity differently.

## Takeaways
One unified relevance model can replace six task-specific ones while improving low-resource tasks through transfer — but the right task-routing mechanism depends on the model family: decoder-only LLMs need explicit task identity (prefixes or private layers) far more than cross-encoders do.
