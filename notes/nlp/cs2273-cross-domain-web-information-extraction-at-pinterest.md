---
id: cs2273
title: Cross-Domain Web Information Extraction at Pinterest
company: Pinterest
primary_category: nlp
sub_category: information-extraction
year: 2025
source_url: https://arxiv.org/abs/2508.01096
tags: [web-extraction, information-extraction, e-commerce, multimodal, xgboost, html, visual, structural, kdd]
---

# Cross-Domain Web Information Extraction at Pinterest
**Pinterest** · 2025 · [source](https://arxiv.org/abs/2508.01096)

## Problem
Pinterest needs structured product data (price, title, availability) extracted from arbitrary e-commerce websites at very high volume. Webpages are unstructured and vary wildly across domains, and LLM-based extraction is far too expensive at the required throughput.

## Approach / System design
A novel webpage representation that fuses three modalities — structural (DOM), visual (style/layout), and textual — into a compact per-node format: each visible HTML node is described by its text, style, and layout information. This rich representation is deliberately designed so that small, cheap models can learn the extraction task. An XGBoost model classifies nodes to extract the target attributes, evaluated against GPT and other LLM baselines.

## Key decisions
- Invest in feature/representation engineering instead of model capacity: encode structure + vision + text per node so a gradient-boosted tree can do the job.
- Choose XGBoost over LLMs for the production path, prioritizing throughput and cost at Pinterest scale.
- Keep the representation compact enough for 1000+ URLs/sec serving.

## Stack
Multimodal (structural + visual + textual) HTML node representation; XGBoost as the production extraction model; GPT and other LLMs as comparison baselines.

## Results
- Throughput over 1,000 URLs per second.
- More accurate attribute extraction than GPT baselines on the cross-domain task.
- ~1000x more cost-effective than the cheapest GPT alternative.

## Takeaways
For high-volume extraction, representation design beats model size: a well-engineered multimodal encoding of the page lets a boosted-tree model outperform LLMs at three orders of magnitude lower cost. LLMs are not the default answer for structured web extraction when throughput and unit economics dominate.
