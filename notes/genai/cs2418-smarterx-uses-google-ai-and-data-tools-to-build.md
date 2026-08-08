---
id: cs2418
title: "SmarterX Uses Google AI and Data Tools to Build Custom LLMs for Regulatory Compliance"
company: SmarterX
primary_category: genai
sub_category: rag
year: 2025
source_url: https://cloud.google.com/blog/products/data-analytics/smarterx-uses-google-ai-and-data-tools-to-build-custom-llms
tags: [custom-llm, compliance, rag, bigquery, vertex-ai, product-data]
---

# SmarterX Uses Google AI and Data Tools to Build Custom LLMs for Regulatory Compliance
**SmarterX** · 2025 · [source](https://cloud.google.com/blog/products/data-analytics/smarterx-uses-google-ai-and-data-tools-to-build-custom-llms)

## Problem
Consumer packaged goods brands and retailers must ensure every product is sold, shipped, stored, and disposed of in compliance with applicable regulations—a task that spans millions of SKUs across multiple sales channels. Regulatory information is scattered across websites, research papers, safety data sheets, and regulatory databases, requiring sophisticated search and parsing strategies to locate and normalize at scale.

## Approach / System design
SmarterX runs a three-phase pipeline: ML and NLP-powered web crawlers locate and ingest regulatory data from diverse sources; BigQuery serves as the processing engine for real-time cleansing, normalization, and schema application at runtime; and Vertex AI hosts multiple discrete customer-specific LLMs, each fine-tuned for a particular regulatory domain so models can be updated independently as requirements change. RAG connects Gemini to proprietary customer databases, grounding outputs in verified sources and providing citations. Google Cloud Workflows orchestrates the overall pipeline, and BigQuery's SQL interface allows domain experts to interact with data and evaluate models without data scientist intermediaries.

## Key decisions
Building separate small LLMs per customer per regulatory domain—rather than one large generalist model—allows independent updates when specific regulations change and reduces the risk of one customer's data affecting another's model behavior. Grounding Gemini outputs through RAG was prioritized for compliance use cases because every claim must be traceable to a verified regulatory source. Adopting a unified Google Cloud stack (BigQuery, Vertex AI, Gemini, Workflows) eliminated context switching between tools and allowed domain-expert subject matter experts to evaluate and deploy models independently.

## Stack
BigQuery (data warehouse and ETL engine), Cloud Storage, Vertex AI (model training and deployment), Gemini (LLM with built-in grounding), Google Cloud Workflows (orchestration), RAG pipeline.

## Results
The platform processes millions of SKUs daily in real-time with automatic scaling. Domain experts can now evaluate, correct, and deploy models without requiring a data scientist as an intermediary, accelerating iteration cycles. Chemistry-specific sub-models handle precise calculations (flashpoints, pH levels, boiling points) where LLM approximation is insufficient.

## Takeaways
Domain-specialized small models maintained independently per regulatory area are more operationally tractable than a single large compliance model, because regulatory changes in one area can be addressed without retraining or risk of regression in unrelated domains. Designing the platform so that non-technical subject matter experts can directly interact with and evaluate models—without a data science intermediary—is a practical multiplier on both iteration speed and organizational buy-in.
