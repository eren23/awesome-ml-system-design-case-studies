---
id: cs0835
title: "Introducing PIXEL: Instacart's Unified Image Generation Platform"
company: Instacart
primary_category: cv
sub_category: image-classification
year: 2025
source_url: https://tech.instacart.com/introducing-pixel-instacarts-unified-image-generation-platform-6d7dd0efe4c1
tags: [CV, product feature]
---

# Introducing PIXEL: Instacart's Unified Image Generation Platform
**Instacart** · 2025 · [source](https://tech.instacart.com/introducing-pixel-instacarts-unified-image-generation-platform-6d7dd0efe4c1)

## Problem
Online grocery customers can't physically inspect products (especially perishables), so image quality directly affects conversion. Inside Instacart, multiple teams were independently experimenting with image-generation models, prompts, and evaluation, causing duplicated effort and inconsistent results.

## Approach / System design
PIXEL is a centralized image-generation platform usable by any Instacart employee regardless of technical depth. It standardizes generation behind a unified parameter protocol across multiple vendor models, ships pre-built prompt templates with few-shot examples tuned for food imagery, supports fine-tuned custom models for Instacart product categories, and adds automated quality evaluation via vision-language models. It integrates into infra as an RPC service backed by S3 and Snowflake.

## Key decisions
- DreamBooth fine-tuning on diffusion models (e.g., Stable Diffusion) for realistic, product-specific generation with re-contextualization.
- Replace labor-intensive manual review with vision-language model feedback loops scoring composition, consistency, style, and appeal.
- Keep the platform multi-model because the best model varied project by project; enable fast experimentation before scaling to production.

## Stack
Diffusion models (Stable Diffusion base) with DreamBooth fine-tuning; vision-language models for automated evaluation; LLM-generated evaluation prompts and prompt refinement; RPC service; S3 and Snowflake storage.

## Results
- ~10x reduction in time-to-generate new imagery.
- Human approval rate of generated images improved from ~20% to ~85%.
- ~25% decrease in navigation time and cart abandonment for butcher cuts.
- ~15% increase in carousel-recommendation conversion for lifestyle imagery.

## Takeaways
Centralizing GenAI behind one platform — standard params, food-tuned prompt templates, fine-tuning, and automated VLM-based evaluation — turns scattered experimentation into a reusable capability and removes the manual-review bottleneck that otherwise gates image quality at scale.
