---
id: cs2322
title: From Pixels to Purchase: Building and Evaluating a Taxonomy-Decoupled Visual Search Engine for Home Goods E-commerce
company: Wayfair
primary_category: cv
sub_category: visual-search
year: 2026
source_url: https://arxiv.org/abs/2601.11769
tags: [visual-search, embeddings, ecommerce, home-goods, taxonomy, production, retrieval]
---

# From Pixels to Purchase: Building and Evaluating a Taxonomy-Decoupled Visual Search Engine for Home Goods E-commerce
**Wayfair** · 2026 · [source](https://arxiv.org/abs/2601.11769)

## Problem
Visual search in style-driven e-commerce is hard because user intent is subjective and open-ended. Conventional systems couple object detection to taxonomy-based classification — detect an object, classify it into a category, then search within that category — which is brittle, noisy, and limits scaling across a broad home-goods catalog.

## Approach / System design
Wayfair built a taxonomy-decoupled visual search engine with two core components:
- **Classification-free region proposals**: candidate regions are proposed without forcing a rigid taxonomy label, removing the classification stage as a failure point.
- **Unified embeddings for retrieval**: a single embedding space handles similarity retrieval across product domains, so matching is driven by visual similarity directly rather than gated by predicted category.
For evaluation, the team built an LLM-as-a-Judge framework that zero-shot assesses visual similarity and category relevance of retrieved results, avoiding dependence on human annotations or catalog metadata. The system was deployed at scale on a global home-goods platform.

## Key decisions
- Decouple retrieval from taxonomy: replace detection→classification→category-restricted search with direct embedding similarity, enabling cross-category generalization.
- Use a unified embedding model instead of per-category models, simplifying the serving surface.
- Evaluate with LLM judges rather than human-annotated ground truth, sidestepping the annotation bottleneck while checking that offline metrics track real outcomes.

## Stack
Region-proposal model (classification-free), unified visual embedding model, embedding-based similarity retrieval, LLM-as-a-Judge evaluation framework. Specific model architectures and serving infrastructure are not detailed in the abstract.

## Results
- Improved retrieval quality over the taxonomy-coupled approach (magnitudes not stated in the abstract).
- A measurable uplift in customer engagement after production deployment.
- Offline LLM-judge evaluation metrics were found to strongly correlate with real-world outcomes.

## Takeaways
- Removing taxonomy coupling makes visual search more general and less brittle — category prediction errors stop propagating into retrieval.
- LLM-based evaluation is a practical substitute for human annotation in visual search, provided its correlation with online metrics is validated.
- A single unified embedding across a heterogeneous catalog can outperform category-specific pipelines while being simpler to operate.
