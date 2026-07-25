---
id: cs2121
title: "PRAGMA: Revolut Foundation Model for Payments and Fraud"
company: Revolut
primary_category: fraud
sub_category: payment-fraud
year: 2026
source_url: https://arxiv.org/abs/2604.08649
tags: [foundation-model, transformer, fraud-detection, payments, large-scale-ml, production-deployment]
---

# PRAGMA: Revolut Foundation Model for Payments and Fraud
**Revolut** · 2026 · [source](https://arxiv.org/abs/2604.08649)

## Problem
Banks and fintechs sit on enormous volumes of transactional and event-level data whose economic signal is largely untapped. Revolut wanted a single representation layer over this heterogeneous banking data that could power many downstream applications (fraud detection, credit scoring, lifetime value) instead of building bespoke models per task.

## Approach / System design
PRAGMA is a transformer-based foundation model trained with a masked-modeling, self-supervised objective on large-scale sequences of banking events. The design is tailored to the discrete, variable-length nature of financial records, ingesting raw multi-source event streams. Per the catalog metadata, training covered roughly 40 billion events from 25 million users. Downstream teams consume the learned embeddings: a simple linear model on top of extracted embeddings already performs strongly, with optional light fine-tuning for further gains.

## Key decisions
- Transformer foundation model with masked modeling rather than per-task supervised architectures.
- Raw multi-source banking event sequences as input, avoiding heavy task-specific feature engineering.
- Serve embeddings as a general-purpose layer; downstream tasks attach linear heads or lightweight fine-tuning.

## Stack
Transformer architecture with self-supervised pretraining; per the catalog metadata, production deployment runs on 200+ H100 GPUs.

## Results
The abstract reports superior performance across multiple financial domains without listing benchmark figures. Per the catalog metadata, the deployed model catches 65% more fraud than prior production models.

## Takeaways
A foundation model over banking event data can serve as a shared representation layer for fraud, credit, and value prediction without task-specific architecture changes — the classic pretrain-once, adapt-cheaply pattern transferred to payments.
