---
id: cs1834
title: Deep Dive in PaddleOCR Inference
company: Adevinta
primary_category: cv
sub_category: ocr
year: 2023
source_url: https://medium.com/adevinta-tech-blog/deep-dive-in-paddleocr-inference-e86f618a0937
tags: [ocr, paddleocr, pp-ocrv3, sagemaker, text-in-image]
---

# Deep Dive in PaddleOCR Inference
**Adevinta** · 2023 · [source](https://medium.com/adevinta-tech-blog/deep-dive-in-paddleocr-inference-e86f618a0937)

## Problem
Adevinta's Cognition CV team needed a reliable OCR service to detect and read text in listing images across its European marketplaces. The existing system required a replacement that could be dependably deployed as a SageMaker endpoint, which meant the OCR pipeline had to integrate cleanly with AWS managed infrastructure.

## Approach / System design
The team rebuilt the "Text in Image" service on PaddleOCR's PP-OCRv3, migrating from a previous OCR approach to take advantage of PP-OCRv3's improved accuracy and performance characteristics. Refactoring focused on the pre-processing and post-processing steps to make them production-ready and compatible with SageMaker endpoint conventions. Unnecessary parameters were pruned to streamline the inference pipeline and reduce deployment complexity.

## Key decisions
PP-OCRv3 was selected from the PaddleOCR family for its balance of accuracy and speed. Deep refactoring of the pre/post-processing code was necessary to make PaddleOCR's reference implementation deployable in a managed cloud endpoint context. Parameter pruning reduced the surface area of the configuration and improved reliability.

## Stack
PaddleOCR PP-OCRv3, AWS SageMaker managed endpoints. Specific serving framework details beyond SageMaker are not covered in the source.

## Results
Not covered in the source.

## Takeaways
Open-source OCR frameworks like PaddleOCR often require significant refactoring of reference implementations before they are suitable for production managed-cloud deployments. Pruning parameters and simplifying pre/post-processing pipelines can be as important as model selection for reliable endpoint operation.
