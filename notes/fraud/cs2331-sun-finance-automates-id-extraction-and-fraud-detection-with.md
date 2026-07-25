---
id: cs2331
title: Sun Finance Automates ID Extraction and Fraud Detection with Generative AI on AWS
company: Sun Finance
primary_category: fraud
sub_category: identity
year: 2026
source_url: https://aws.amazon.com/blogs/machine-learning/sun-finance-automates-id-extraction-and-fraud-detection-with-generative-ai-on-aws/
tags: [genai, document-fraud, identity-verification, aws-bedrock, ocr, computer-vision]
---

# Sun Finance Automates ID Extraction and Fraud Detection with Generative AI on AWS
**Sun Finance** · 2026 · [source](https://aws.amazon.com/blogs/machine-learning/sun-finance-automates-id-extraction-and-fraud-detection-with-generative-ai-on-aws/)

## Problem
Sun Finance, a Latvian fintech processing over 4M loan evaluations monthly, had a KYC bottleneck: about 60% of applications needed manual review, and roughly 80% of those stemmed from OCR extraction errors rather than customer mistakes. The system had to handle seven ID document types across multiple languages and catch fraud attempts (about 10% of daily requests). Manual processing costs also blocked expansion into lower-value microloan markets where unit economics couldn't absorb human review.

## Approach / System design
Two parallel serverless pipelines were built in a 6-week engagement:
- **ID extraction pipeline**: Amazon Textract as primary OCR; Amazon Rekognition as fallback OCR for low-confidence extractions; Claude Sonnet 4 via Amazon Bedrock structures the raw text into standardized JSON; a validation layer applies formatting checks, date standardization, and document-type normalization.
- **Fraud detection pipeline** (orchestrated by AWS Step Functions, running checks in parallel):
  - Visual pattern detection: Claude analyzes selfies for screen re-photography, glare, and digital manipulation.
  - Background similarity: Rekognition masks faces, Amazon Titan Multimodal Embeddings produces 1024-dimensional vectors, and Amazon S3 Vectors performs similarity search against known fraud patterns (e.g., fraud rings reusing backgrounds).
  - Risk assessment combines the two scores with 50/50 weighting into high/medium/low confidence classifications.
The architecture evolved through three iterations: Claude alone hit 61.8% accuracy (its PII safety behavior resisted processing identity documents); Textract + Claude reached 85%; adding the Rekognition fallback tier and validation rules reached 90.8%.

## Key decisions
- "OCR + LLM beats LLM alone": specialized OCR handles character recognition; the LLM handles contextual structuring and normalization.
- Visual embeddings over text embeddings for background matching — visual scored 96% accuracy / 80% precision / 52% recall vs. text's 91% / 27.8% / 21.7%.
- Parallel Step Functions execution cut fraud-check latency from 6–8s to 3–5s (~40% improvement).
- Reserve expensive LLM calls for high-value steps and use cheaper specialized services first, driving the 91% per-document cost reduction.
- Modular Lambda functions allowed weekly architectural pivots during the engagement without production downtime.

## Stack
AWS Lambda, Step Functions, API Gateway, Amazon Bedrock (Anthropic Claude Sonnet 4, Amazon Titan Multimodal Embeddings), Amazon Textract, Amazon Rekognition, Amazon S3 Vectors, Cognito (SigV4 auth), AWS WAF, AWS KMS.

## Results
- Overall extraction accuracy: 79.7% → 90.8%; ID-number extraction 74.3% → 89.4%; document-type identification 78.4% → 96.4%.
- Processing time: up to ~20 hours → under 5 seconds.
- Per-document cost down 91%; manual review rate projected to halve from 60% to 30% (staffing ~3 FTEs → ~1 FTE for this workload).
- Fraud detection: 81% accuracy, 59% recall, 83% specificity; screen-photo detection at 95%+ confidence; recall on seen fraud patterns 55% vs. 16.7% on novel patterns, improving as confirmed cases populate the vector database.
- Regional expansion into microloan markets became economically viable.

## Takeaways
- Separation of concerns wins: specialized OCR + LLM structuring + rule-based validation outperformed a monolithic LLM approach by ~29 accuracy points.
- LLM safety guardrails can be a real integration constraint — Claude's PII protections initially blocked direct ID processing and shaped the architecture.
- Multi-method fraud detection is necessary: visual pattern checks catch presentation attacks while embedding similarity catches fraud rings, and neither suffices alone.
- A reference vector database of confirmed fraud grows more valuable over time; planned upgrades include EXIF/geolocation/device-fingerprint signals.
