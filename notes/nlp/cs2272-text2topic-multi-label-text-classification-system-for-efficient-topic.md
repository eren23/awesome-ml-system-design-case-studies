---
id: cs2272
title: Text2Topic: Multi-Label Text Classification System for Efficient Topic Detection in User Generated Content with Zero-Shot Capabilities
company: Booking.com
primary_category: nlp
sub_category: entity-resolution
year: 2023
source_url: https://aclanthology.org/2023.emnlp-industry.10/
tags: [text-classification, multi-label, topic-detection, bi-encoder, zero-shot, transformer, hotel-reviews, stream-processing]
---

# Text2Topic: Multi-Label Text Classification System for Efficient Topic Detection in User Generated Content with Zero-Shot Capabilities
**Booking.com** · 2023 · [source](https://aclanthology.org/2023.emnlp-industry.10/)

## Problem
Booking.com needed to extract structured topic information from large volumes of user-generated text (hotel reviews, forum posts) — a multi-label classification problem over hundreds of topics that must run efficiently at production scale and adapt to new topics without retraining.

## Approach / System design
Text2Topic uses a Bi-Encoder Transformer architecture that encodes the text and the topic separately, then combines the embeddings via concatenation, subtraction, and multiplication before scoring. Because topics are encoded rather than fixed output classes, the system supports zero-shot prediction on unseen topics. The design produces domain-specific embeddings and enables high-throughput batch inference, and the model is deployed on a real-world stream processing platform.

## Key decisions
- Bi-encoder over cross-encoder/classifier-head designs to get zero-shot topic support and cheap batch scoring.
- Embedding interaction features (concat, subtract, multiply) on both text and topic sides, validated with ablation studies.
- Smart sampling and partial-labeling strategies to keep annotation cost manageable across 239 topics.
- Benchmarked against state-of-the-art baselines including LLMs before committing to the deployed architecture.

## Stack
Bi-Encoder Transformer; training corpus of ~1.6M text-topic pairs (~200K positive annotations) over ~120K texts from three Booking.com data sources; deployed on a stream processing platform for batch inference. Published at EMNLP 2023 Industry Track.

## Results
- 92.9% micro mAP and 75.8% macro mAP across 239 topics.
- Zero-shot capability for new topics without retraining.
- Runs in production on Booking.com's stream processing platform.

## Takeaways
A carefully engineered bi-encoder gives a practical middle ground for industrial multi-label classification: near-SOTA accuracy, high-throughput inference, and zero-shot extensibility that classifier-head architectures lack. Annotation strategy (sampling, partial labels) matters as much as architecture when the label space is in the hundreds.
