---
id: cs2365
title: Complicated Semantic Alignment for Long-Tail Query Rewriting in Taobao Search Based on Large Language Model
company: Taobao
primary_category: search
sub_category: semantic-search
year: 2025
source_url: https://dl.acm.org/doi/10.1145/3711896.3737204
tags: [llm, query-rewriting, semantic-alignment, long-tail, e-commerce-search, cross-semantic]
---

# Complicated Semantic Alignment for Long-Tail Query Rewriting in Taobao Search Based on Large Language Model
**Taobao** · 2025 · [source](https://dl.acm.org/doi/10.1145/3711896.3737204)

## Problem
Long-tail queries with complicated semantics still fail in Taobao search: users' natural-language phrasing does not match merchant product naming conventions, and prior LLM-based rewriting methods — lacking e-commerce fine-tuning and alignment training — can hallucinate, producing rewrites that are semantically correct yet retrieve no products.

## Approach / System design
The paper (KDD 2025) proposes the Complicated Semantic Alignment Query Rewrite (CSA-QR) framework, operating in three stages. First, a high-quality SFT dataset is built: LLMs generate rewrite candidates, humans annotate them, and retrieval-augmented generation produces improved training data. Second, a multi-dimensional alignment dataset is collected, decoupling feedback into two dimensions — consistency with user semantics and consistency with merchant expression. Third, a reward model trained with a binary feedback method guides PPO-based reinforcement alignment, with purpose-built reward-model evaluation metrics steering iterative improvement.

## Key decisions
- Decouple alignment feedback into user-semantic consistency and merchant-expression consistency instead of a single monolithic quality score.
- Train the reward model with binary feedback, found better suited to this rewriting context than alternatives.
- Use retrieval-augmented generation plus human annotation to construct the SFT data, targeting rewrites that both preserve meaning and actually retrieve products.
- Design custom evaluation metrics for the reward model to guide alignment iterations.

## Stack
Not covered in the source beyond the LLM + reward model + PPO alignment pipeline.

## Results
Offline experiments showed improved retrieval performance. Online A/B tests on Taobao showed significant improvements in product click-through rate, GMV, and transaction count for long-tail queries. The system has been deployed in production since September 2024.

## Takeaways
For e-commerce rewriting, "semantically correct" is not enough — a rewrite must also match how merchants actually describe products. Splitting the alignment objective along those two axes, and training a reward model to enforce both, is what closed the gap that earlier single-objective LLM rewriters (including the team's prior work) left open.
