---
id: cs2361
title: "BEQUE: Large Language Model based Long-tail Query Rewriting in Taobao Search"
company: Taobao
primary_category: search
sub_category: semantic-search
year: 2024
source_url: https://arxiv.org/abs/2311.03758
tags: [llm, query-rewriting, long-tail, e-commerce-search, recall-improvement]
---

# BEQUE: Large Language Model based Long-tail Query Rewriting in Taobao Search
**Taobao** · 2024 · [source](https://arxiv.org/abs/2311.03758)

## Problem
Long-tail queries on Taobao suffer from "few-recall": infrequent, specific searches fail to match relevant products because of semantic gaps between how users phrase queries and how merchants describe listings. Rewriting these queries into forms the retrieval system understands is the lever, but generic LLM rewrites are not aligned with e-commerce retrieval behavior.

## Approach / System design
BEQUE (WWW 2024) is a three-stage LLM pipeline. Stage 1: multi-instruction supervised fine-tuning on a rewriting dataset constructed with rejection sampling and auxiliary-task mixing. Stage 2: offline feedback — beam search generates multiple candidate rewrites per query, which are fed through Taobao's offline retrieval system to obtain partial-order ranking signals reflecting actual retrieval outcomes. Stage 3: objective alignment — contrastive learning over the ranked rewrites aligns the model with Taobao's business metrics (GMV, transactions, visitors) rather than with surface-level rewrite quality.

## Key decisions
- Fine-tune the LLM specifically for e-commerce rewriting instead of prompting a general model.
- Use the production retrieval system offline as the judge of rewrite quality, producing partial-order feedback grounded in what actually gets recalled.
- Align with ranking signals via contrastive learning rather than binary good/bad labels.
- Validate offline before deployment, then measure with online A/B tests on business metrics.

## Stack
Not covered in the source beyond the LLM fine-tuning pipeline and Taobao's offline retrieval system used for feedback.

## Results
Offline experiments showed the framework effectively bridges semantic gaps for long-tail queries. Online A/B testing showed significant boosts to GMV, transaction count, and unique visitors on long-tail queries. BEQUE has been deployed on Taobao since October 2023.

## Takeaways
The critical ingredient for production query rewriting is grounding the LLM in the retrieval system's actual behavior: rewrites must be judged by what they recall, not by how good they look. A staged pipeline — SFT, system-in-the-loop feedback, then metric-aligned contrastive tuning — turns a generic LLM into a component that moves business metrics.
