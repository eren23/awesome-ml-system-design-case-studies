---
id: cs2087
title: Multi-gate-Mixture-of-Experts (MMoE) model architecture and knowledge distillation in Ads Engagement modeling development
company: Pinterest
primary_category: ads
sub_category: ctr-prediction
year: 2025
source_url: https://medium.com/pinterest-engineering/multi-gate-mixture-of-experts-mmoe-model-architecture-and-knowledge-distillation-in-ads-08ec7f4aa857
tags: [MMoE, knowledge-distillation, ads-engagement, multi-task, latency, inference-optimization]
---

# Multi-gate-Mixture-of-Experts (MMoE) model architecture and knowledge distillation in Ads Engagement modeling development
**Pinterest** · 2025 · [source](https://medium.com/pinterest-engineering/multi-gate-mixture-of-experts-mmoe-model-architecture-and-knowledge-distillation-in-ads-08ec7f4aa857)

## Problem
Pinterest's ads engagement ranking model hit two walls: the existing DCNv2 shared-bottom architecture stopped scaling (adding layers/parameters no longer bought proportional metric gains), and short data-retention windows (months to a year) meant new experimental models could not train on the historical data the production model had seen, making comparisons unfair and losing accumulated knowledge.

## Approach / System design
Two-part solution. (1) MMoE: replace the monolithic shared-bottom with multiple expert networks, each specializing in different aspects of the data, with per-task gate networks that route inputs to the right experts — dynamic capacity allocation across tasks. (2) Knowledge distillation: during batch training, add a supplementary loss that teaches the experimental model to match the production model's predictions, effectively transferring knowledge learned from since-deleted historical data. To pay for MMoE's extra compute, the team applied mixed-precision inference and kept gate layers lightweight.

## Key decisions
- DCNv2 as the expert architecture: benchmarked against MaskNet and FinalMLP, DCNv2 experts gave the best return on investment.
- Distill only during batch training; applying distillation in incremental training caused overfitting, so it was removed there.
- Pairwise-style loss for distillation from the production teacher.
- Offset MMoE serving cost with mixed-precision inference (40% latency reduction) and lightweight gates rather than shrinking the experts.

## Stack
DCNv2-based experts inside an MMoE framework, knowledge distillation from the production model, mixed-precision inference for serving. Specific training frameworks are not covered in the source.

## Results
On a system where a 0.1% offline accuracy improvement is considered significant, the MMoE + distillation model delivered "very significant" offline and online gains on RelatedPins and Search surfaces, alongside a 40% inference latency reduction from mixed-precision serving.

## Takeaways
When a shared-bottom model stops scaling, moving capacity into gated experts restores headroom; and distillation from the production model is a practical answer to data-retention limits — the teacher becomes the archive of the deleted training data. Serving-cost engineering (precision, gate size) is what makes the architecture shippable.
