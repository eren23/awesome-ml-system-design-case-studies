---
id: cs2404
title: How Thomson Reuters Accelerated Research and Development of Natural Language Processing Solutions with Amazon SageMaker
company: Thomson Reuters
primary_category: nlp
sub_category: entity-resolution
year: 2021
source_url: https://aws.amazon.com/blogs/machine-learning/how-thomson-reuters-accelerated-research-and-development-of-natural-language-processing-solutions-with-amazon-sagemaker/
tags: [information-extraction, entity-recognition, text-classification, sagemaker, legal-text, multi-task-learning]
---

# How Thomson Reuters Accelerated Research and Development of Natural Language Processing Solutions with Amazon SageMaker
**Thomson Reuters** · 2021 · [source](https://aws.amazon.com/blogs/machine-learning/how-thomson-reuters-accelerated-research-and-development-of-natural-language-processing-solutions-with-amazon-sagemaker/)

## Problem
Thomson Reuters Labs wanted to rapidly prototype machine reading comprehension and question-answering systems over proprietary legal and tax content — hundreds of thousands of QA pairs — but traditional approaches implied 15–18 months of R&D and heavy upfront GPU investment. They needed fast, cost-controlled experimentation with large BERT variants while keeping proprietary data access compliant.

## Approach / System design
The team ran model development, training, and inference on Amazon SageMaker. To reconcile cloud convenience with security requirements, they built Secure Content Workspace (SCW), an internal web tool that provisions SageMaker resources with controlled, compliant access to proprietary datasets. QA quality prediction was formulated as binary classification over subject-matter-expert-graded QA pairs (grades A, C, D, F).

## Key decisions
- Experiment across BERT sizes: base (12 layers, ~100M parameters) up to large variants (24 layers, ~300M parameters).
- GPU flexibility: V100s with 32GB memory for the largest models, moving between P2, P3, and G4 instance families as workloads demanded.
- Both TensorFlow and PyTorch supported for deep learning work.
- SageMaker Managed Spot Instances for training to cut cost.
- Wrap cloud resource provisioning in SCW so security/compliance is enforced by the platform, not by individual researchers.

## Stack
Amazon SageMaker, V100/P3/P2/G4 GPU instances, TensorFlow, PyTorch, custom Secure Content Workspace wrapper.

## Results
- Fine-tuning time shrank from many hours to under 1 hour.
- Pretraining reduced from an estimated several weeks to a few days.
- Spot training cut training costs by 40–50% on average (up to ~50% in specific cases).
- The resulting system was expected to handle millions of requests per day in production.

## Takeaways
- Managed ML services let a research lab experiment with large transformers without owning GPU infrastructure or waiting on procurement.
- Pay-as-you-go plus automatic resource cleanup fits the bursty nature of exploratory research.
- An internal security wrapper is a practical bridge between cloud agility and enterprise compliance.
- Transfer learning and domain adaptation unlocked specialized legal/tax NLP from general-purpose pretrained models.
