---
id: cs2271
title: Building Bilingual NER for Cargo Logistics with Amazon Bedrock
company: IBS Software
primary_category: nlp
sub_category: entity-resolution
year: 2026
source_url: https://aws.amazon.com/blogs/machine-learning/building-bilingual-ner-for-cargo-logistics-with-amazon-bedrock/
tags: [ner, bilingual, model-distillation, amazon-bedrock, cargo-logistics, knowledge-distillation, japanese, english]
---

# Building Bilingual NER for Cargo Logistics with Amazon Bedrock
**IBS Software** · 2026 · [source](https://aws.amazon.com/blogs/machine-learning/building-bilingual-ner-for-cargo-logistics-with-amazon-bedrock/)

## Problem
IBS Software processes thousands of cargo logistics emails daily in English and Japanese, needing to extract 23 entity types (AWB numbers, flight details, weights, delivery instructions). Manual handling slowed operations, and building an NER solution meant trading off accuracy (large models, high cost) against economics (small models, lower accuracy).

## Approach / System design
An event-driven extraction pipeline: emails land as .eml files in Amazon S3, AWS Lambda extracts the content, an Amazon Bedrock endpoint runs NER inference, and structured JSON is written to DynamoDB — end-to-end in under 2 seconds. The model is produced via Amazon Bedrock Model Distillation: Amazon Nova Pro acts as the teacher, distilled into a Nova Lite student using token-level KL-divergence loss, trained on 500 manually annotated bilingual emails (350 English, 150 Japanese) labeled by domain experts.

## Key decisions
- Abandoned an initial open-source distillation route (PyTorch + TextBrewer) due to framework complexity, lack of managed infrastructure, and hyperparameter tuning difficulty — pivoted to Bedrock's managed distillation.
- Chose Nova Pro → Nova Lite distillation to keep near-teacher accuracy at a fraction of inference cost.
- Invested in expert manual annotation of a small (500-email) but high-quality bilingual dataset.
- Training configuration: 4 epochs, 70 training steps, 2048 max sequence length.

## Stack
Amazon Bedrock Model Distillation (teacher: Amazon Nova Pro v1; student: Amazon Nova Lite v1), Amazon S3, AWS Lambda, Amazon DynamoDB.

## Results
- 95.085% overall F1 (96.535% English, 93.635% Japanese); the Japanese gap is attributed to kanji complexity and the smaller Japanese training set.
- Student retained 98% of teacher performance.
- 14x reduction in inference cost; sub-2-second end-to-end processing.
- Training loss fell from 0.05 to 0.008; delivered in 4 months by a team of 9.

## Takeaways
Managed distillation services can remove the main operational barrier to teacher-student compression — the team's open-source attempt failed on infrastructure complexity, not on the technique. A few hundred expert-annotated examples suffice to distill a specialized bilingual NER model, but per-language data balance directly shows up in per-language F1.
