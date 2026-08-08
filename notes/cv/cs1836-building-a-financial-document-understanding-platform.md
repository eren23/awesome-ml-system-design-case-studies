---
id: cs1836
title: Building a Financial Document Understanding Platform
company: Intuit
primary_category: cv
sub_category: ocr
year: 2019
source_url: https://medium.com/intuit-engineering/building-a-financial-document-understanding-platform-9e42f7d497c
tags: [document-ai, ocr, layout-analysis, bert, cnn-classification]
---

# Building a Financial Document Understanding Platform
**Intuit** · 2019 · [source](https://medium.com/intuit-engineering/building-a-financial-document-understanding-platform-9e42f7d497c)

## Problem
Intuit's users submit diverse financial documents — tax forms, receipts, bank statements — that need to be automatically read, classified, and have key fields extracted to power products like TurboTax. Manual document processing is too slow and costly for the scale and variety of documents encountered, and the high accuracy required for financial data makes this a demanding problem.

## Approach / System design
The Document Understanding Platform chains four stages: OCR converts document images to text, a CNN classifier identifies the document type (trained by transfer learning from ImageNet through RVL-CDIP to Intuit-specific document types), layout analysis locates fields and regions on the page, and a BERT-based model extracts the values of relevant fields. A user-feedback loop captures corrections on extracted fields and feeds them back into model retraining, enabling continuous improvement.

## Key decisions
Transfer learning for document classification — ImageNet to RVL-CDIP to internal data — reduces the labeled data requirement for Intuit-specific document types. Using BERT for information extraction leverages language context to improve accuracy over pure rule-based approaches. Closing the loop with user corrections ensures the system improves on the specific documents and errors it encounters in production.

## Stack
OCR engine, CNN for document classification (ImageNet/RVL-CDIP transfer learning), layout analysis module, BERT (field extraction), user-feedback retraining loop. Specific infrastructure details are not covered in the source.

## Results
The BERT-based extraction stage achieves approximately 93% accuracy. The full pipeline spans document classification through field-level extraction.

## Takeaways
Layering OCR, classification, layout analysis, and NLP extraction in a sequential pipeline is an effective architecture for document understanding, with each stage reducing the complexity of the next. Closing the production loop with user-feedback retraining is essential for maintaining accuracy across the diverse and evolving document types encountered in a large consumer financial platform.
