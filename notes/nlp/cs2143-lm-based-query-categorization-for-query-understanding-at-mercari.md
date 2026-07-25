---
id: cs2143
title: LM-Based Query Categorization for Query Understanding at Mercari
company: Mercari
primary_category: nlp
sub_category: classification
year: 2023
source_url: https://engineering.mercari.com/en/blog/entry/20231222-language-model-based-query-categorization-for-query-understanding/
tags: [query-understanding, text-classification, distilbert, search, query-categorization, production, marketplace]
---

# LM-Based Query Categorization for Query Understanding at Mercari
**Mercari** · 2023 · [source](https://engineering.mercari.com/en/blog/entry/20231222-language-model-based-query-categorization-for-query-understanding/)

## Problem
Mercari's US search needs to classify user queries into a target taxonomy to improve relevance. Hand-maintained rule mappings are easy to build and explain but require constant review as query patterns shift and new products launch, and can never cover the full query space.

## Approach / System design
The team compared three approaches:
- **Rule-based:** map lookups — explainable, cheap, but high-maintenance and low coverage.
- **Classic ML:** multi-class classifiers trained on query and click logs, reaching 0.72 micro-F1.
- **Language model:** DistilBERT fine-tuned on the same query/click logs, training only the classification layer.

The DistilBERT model won and shipped to production.

## Key decisions
- Chose DistilBERT over classic ML for context sensitivity, availability of pre-trained variants, and robustness to unseen queries — accepting a trade of domain-specificity for versatility.
- Fine-tuned only the classification head, keeping training cost low.
- Sourced supervision from query and click logs rather than manual labels.

## Stack
DistilBERT (fine-tuned classification layer); benchmarked against logistic regression, SVMs, XGBoost, fastText, and an attentional CNN.

## Results
- 0.80 micro-F1 on test data vs 0.72 for the prior ML model.
- Online A/B test: roughly 2x coverage of converted/classified search keywords versus the baseline.

## Takeaways
- A small pre-trained LM gave a meaningful lift over traditional ML at practical implementation cost.
- Pre-training pays off most on unknown/tail queries where rules and log-trained classifiers fail.
- The team sees LM-based query understanding as well-positioned as search shifts toward vector-based retrieval.
