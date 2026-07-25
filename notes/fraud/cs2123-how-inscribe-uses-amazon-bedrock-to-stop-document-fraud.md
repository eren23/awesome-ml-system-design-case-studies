---
id: cs2123
title: How Inscribe Uses Amazon Bedrock to Stop Document Fraud in Seconds
company: Inscribe
primary_category: fraud
sub_category: identity
year: 2024
source_url: https://aws.amazon.com/blogs/machine-learning/how-inscribe-uses-amazon-bedrock-to-stop-document-fraud-in-seconds/
tags: [document-fraud, llm, agentic-ai, amazon-bedrock, identity-verification, automation]
---

# How Inscribe Uses Amazon Bedrock to Stop Document Fraud in Seconds
**Inscribe** · 2024 · [source](https://aws.amazon.com/blogs/machine-learning/how-inscribe-uses-amazon-bedrock-to-stop-document-fraud-in-seconds/)

## Problem
Document fraud is escalating for financial institutions — appearing in roughly 1 in 16 documents, with AI-generated forgeries growing 5x between April and December 2025. Manual review takes about 30 minutes per application, cannot scale with volume, and misses sophisticated deepfakes and coordinated fraud rings; static rule-based systems cannot adapt to evolving tactics.

## Approach / System design
Inscribe built an agentic AI system that works like an expert fraud analyst: it decomposes complex review into steps, coordinates multiple models, calls external APIs (including web search), and produces audit-ready decisions without human intervention — completing analysis in under 90 seconds versus 30 minutes manually. Documents flow in via S3/CloudFront behind a load balancer, get queued in SQS, and are processed by Celery workers on EC2, with Textract handling OCR. Bedrock-hosted LLMs do the reasoning while proprietary forensic and pixel-level models on SageMaker handle image-level fraud signals; a vector database supports retrieval.

## Key decisions
- Multi-model, task-fit routing instead of a single model: Claude Haiku 4.5 for routine parsing/classification/pre-screening (a 40% cost reduction vs. Sonnet), Meta Llama models for transaction analysis and entity extraction, and Claude Sonnet 4/4.5 as the coordination layer for cross-document pattern detection and web-search integration.
- Combine LLM reasoning with proprietary custom CV/forensic models rather than relying on LLMs alone.
- Managed, serverless-style scaling so the team focuses on fraud domain expertise, with elasticity from 10 to 10,000 applications.
- Audit trails and explainability built in for compliance.

## Stack
Amazon Bedrock (Claude Haiku 4.5, Claude Sonnet 4/4.5, Llama), Amazon SageMaker (custom forensic/pixel-analysis models), Amazon Textract, S3, CloudFront, ALB, SQS, EC2 with Celery, RDS, ElastiCache for Valkey, MemoryDB (vector database), CloudWatch.

## Results
About 20x faster than manual review. Customer outcomes: BHG Financial saw 90%+ reduction in manual review time and millions in prevented fraud losses; Logix Federal Credit Union prevented $3M+ fraud in 8 months with up to 99% review-time reduction; BCU prevented $5.6M in fraud losses and detected coordinated fraud rings across applications.

## Takeaways
Agentic architectures let fraud detection adapt to tactics beyond the training data, and deliberate model-tier selection through a unified API cuts cost without hurting accuracy. Pairing LLM coordination with specialized custom models covers what neither can do alone, while managed infrastructure absorbs volume elasticity.
