---
id: cs2117
title: "Machine Learning at Shopify: Tabular Transformer for Merchant GMV Forecasting"
company: Shopify
primary_category: forecast
sub_category: time-series
year: 2025
source_url: https://shopify.engineering/machine-learning-at-shopify
tags: [gmv-forecasting, tabular-transformer, e-commerce, risk-assessment, human-in-the-loop, merchant-capital, ml-platform, applied-ml, llm, personalization, infrastructure, scale]
---

# Machine Learning at Shopify: Tabular Transformer for Merchant GMV Forecasting
**Shopify** · 2025 · [source](https://shopify.engineering/machine-learning-at-shopify)

## Problem
Shopify frames commerce as a giant optimization problem that ML decomposes across the merchant journey. For Shopify Capital specifically, the problem is assessing merchant creditworthiness and long-term earning potential so merchants can get capital quickly and on favorable terms — which requires forecasting each merchant's future Gross Merchandise Volume (GMV).

## Approach / System design
Shopify built a tabular transformer model to forecast merchant GMV, adapting transformer-for-tabular-data methodologies from three academic papers (arXiv 1908.07442 — TabNet lineage, 2201.12886, and 2107.07511) to its commerce-specific datasets. The GMV forecasts underpin Shopify Capital's lending decisions. The article situates this within Shopify's broader ML portfolio: product classification on Qwen multimodal models running hundreds of millions of inferences a day, fraud detection, the Sidekick merchant AI assistant, Nomic-based product embeddings, and experimentation with the HSTU architecture for behavior sequence modeling.

## Key decisions
- Use a transformer architecture on tabular merchant data rather than classical gradient-boosted approaches, adapting published tabular-transformer research to commerce data.
- Treat Shopify's proprietary commerce data and compute infrastructure as the durable differentiators.
- Diversify infrastructure: GCP as the primary partner plus neo-cloud providers (Nebius) for training clusters, CentML for GPU acceleration, and Toloka for data labeling.

## Stack
Tabular transformer models for GMV forecasting; GCP plus Nebius training clusters; CentML for GPU acceleration; Toloka for labeling; Qwen multimodal models and Nomic embeddings elsewhere in the ML portfolio.

## Results
No specific accuracy metrics or business impact numbers for the GMV forecasting model are given in the article.

## Takeaways
Shopify's bet is that data advantage plus computational infrastructure — not any single model — is the moat, with modern architectures (tabular transformers, multimodal LLMs, HSTU) layered on top of commerce-specific datasets. Capital lending pairs the model's forecasts with human review rather than fully automating credit decisions.
