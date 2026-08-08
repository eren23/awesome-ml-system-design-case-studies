---
id: cs2415
title: "Deutsche Bank Delivers AI-Powered Financial Research with DB Lumina"
company: Deutsche Bank
primary_category: genai
sub_category: rag
year: 2025
source_url: https://cloud.google.com/blog/topics/financial-services/deutsche-bank-delivers-ai-powered-financial-research-with-db-lumina
tags: [rag, financial-research, vertex-ai, enterprise-llm, document-retrieval]
---

# Deutsche Bank Delivers AI-Powered Financial Research with DB Lumina
**Deutsche Bank** · 2025 · [source](https://cloud.google.com/blog/topics/financial-services/deutsche-bank-delivers-ai-powered-financial-research-with-db-lumina)

## Problem
Deutsche Bank's research analysts spent substantial time on manual data gathering—sifting through financial statements, SEC filings, regulatory documents, and industry reports—leaving less capacity for strategic analysis and limiting the breadth of topics each analyst could cover. Standard off-the-shelf AI tools did not meet the bank's compliance, data privacy, and domain accuracy requirements for a regulated financial institution.

## Approach / System design
DB Lumina is built on three capabilities: a conversational interface powered by Gemini models for summarization, translation, and drafting; prompt templates for repeatable document-processing workflows; and a RAG system that retrieves from both internal research and external documents such as SEC filings, with inline citations linking responses to source passages. The RAG pipeline uses Dataflow for document ingestion and embedding, Cloud SQL with pgvector and Vertex AI Vector Search for retrieval, and a custom evaluation framework combining automated metrics (citation precision and recall, hallucination detection via Ragas) with human review for tone and content fidelity.

## Key decisions
RAG was chosen over fine-tuning to keep responses grounded in up-to-date enterprise documents without requiring model retraining cycles. Guardrails and audit logging were built in from the start to satisfy regulatory compliance requirements. The platform was rolled out in a phased manner, starting with a pilot of approximately 5,000 users in Investment Bank Origination and Advisory before expanding further.

## Stack
Vertex AI (Gemini 2.0/2.5, Gemini Embeddings API), Google Kubernetes Engine, Cloud SQL with pgvector, Vertex AI Vector Search, Discovery Engine API, Dataflow, Cloud Storage, Cloud Natural Language API, BigQuery, Ragas evaluation framework.

## Results
Analysts saved 30–45 minutes per earnings note template and up to 2 hours per research report or roadshow update. One analyst increased the scope of their earnings report analysis by 50% by adding regional sections and forecast change summaries. The platform was deployed to roughly 5,000 users at the time of publication, with planned expansion to over 10,000.

## Takeaways
RAG grounded in enterprise document stores is well-suited for regulated industries because it provides verifiable citations and can be updated with fresh data without retraining the underlying model. Domain-specific evaluation metrics—citation precision, false rejection rates, hallucination rates—are essential because generic benchmarks do not capture what matters most for financial research quality.
