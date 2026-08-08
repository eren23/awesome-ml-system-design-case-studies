---
id: cs1838
title: Learning Information Extraction from Images of Structured Documents Using Synthetic Data and Conditional Random Fields
company: Intuit
primary_category: cv
sub_category: ocr
year: 2019
source_url: https://www.intuit.com/blog/innovative-thinking/learning-information-extraction-from-images-of-structured-documents-using-synthetic-data-and-conditional-random-field/
tags: [document-ai, synthetic-data, crf, information-extraction, ocr]
---

# Learning Information Extraction from Images of Structured Documents Using Synthetic Data and Conditional Random Fields
**Intuit** · 2019 · [source](https://www.intuit.com/blog/innovative-thinking/learning-information-extraction-from-images-of-structured-documents-using-synthetic-data-and-conditional-random-field/)

## Problem
Extracting specific fields from structured financial documents like W-2 forms and receipts requires labeled training data, but manually annotating large volumes of real tax documents is expensive, privacy-sensitive, and slow. A method was needed to train high-accuracy extraction models without relying heavily on hand-labeled real documents.

## Approach / System design
The team learns the statistical distributions of real document layouts and field values, then uses those distributions to generate large volumes of synthetic labeled document images. These synthetic documents are used to train a Named Entity Recognition model formulated as a Conditional Random Field (CRF), which treats field extraction as a sequence labeling problem over OCR-output tokens. The trained system is deployed in production via Docker containers on AWS.

## Key decisions
Generating synthetic data by learning real-data distributions rather than hand-crafting templates is key to producing training images that reflect the statistical variation of actual documents. The CRF formulation for NER-style sequence labeling captures dependencies between adjacent tokens, which is important for fields that span multiple tokens or require context to identify correctly. Dockerized deployment on AWS provides reproducibility and scalability.

## Stack
Synthetic data generation (distribution-learned document rendering), OCR, CRF-based NER for sequence labeling, Docker, AWS. Specific OCR engine details are not covered in the source.

## Results
Not covered in the source.

## Takeaways
Synthetic data generation that mimics real-document distributions is a powerful strategy for bypassing the annotation bottleneck in document AI, especially when real data carries privacy constraints. CRF-based sequence labeling remains an effective approach for structured extraction tasks where token-level context and field boundaries matter.
