---
id: cs2231
title: Improving Rovo Quality with ML Classifiers
company: Atlassian
primary_category: genai
sub_category: eval
year: 2025
source_url: https://www.atlassian.com/blog/atlassian-engineering/ml-classifier-improving-quality
tags: [ml-classifier, quality-improvement, rovo, evaluation, llm]
---

# Improving Rovo Quality with ML Classifiers
**Atlassian** · 2025 · [source](https://www.atlassian.com/blog/atlassian-engineering/ml-classifier-improving-quality)

## Problem
Atlassian's LLM-based code reviewer agent demonstrably cut PR cycle time (~30%), but its raw output was noisy: overly critical, sometimes factually wrong review comments frustrated users. The team needed a way to surface only the comments likely to be useful.

## Approach / System design
A two-stage pipeline: (1) an LLM (initially GPT-4o, later Claude Sonnet 3.5) generates review comments from code diffs and metadata; (2) a fine-tuned ML classifier — the "comment ranker" — scores each comment on its likelihood of driving an actual code change, and only high-confidence comments are shown. Ground truth comes from user behavior: "code resolution," i.e., whether the PR author actually modified code in response to a comment. The classifier is a fine-tuned ModernBERT model trained on 53,000+ internally labeled code review comments.

## Key decisions
- Move from heuristic/LLM-based comment categorization to a data-driven learned filter.
- Define ground truth behaviorally (code resolution) instead of via subjective manual labels.
- Use a small fine-tuned transformer (ModernBERT) for classification rather than another LLM call.
- Decouple the quality filter from the generative model so the ranker survives LLM swaps.

## Stack
ModernBERT from HuggingFace fine-tuned with GPU acceleration and standard NLP preprocessing (tokenization plus a classification head); GPT-4o and Claude Sonnet 3.5 as the underlying comment generators.

## Results
Code Resolution Rate improved to 40–45%, approaching the ~45% human reviewer benchmark. CRR stayed stable across the GPT-4o → Claude Sonnet 3.5 transition. The system serves 400+ external beta customers and reviews 43,000+ PRs monthly.

## Takeaways
User behavior data beat manual labeling as a training signal. Because the filtering layer is independent of the generator, it outlasts LLM changes — and the proprietary behavioral dataset becomes a durable moat rather than relying only on foundation-model improvements.
