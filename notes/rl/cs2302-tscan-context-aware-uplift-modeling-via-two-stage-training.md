---
id: cs2302
title: "TSCAN: Context-Aware Uplift Modeling via Two-Stage Training for Online Merchant Business Diagnosis"
company: Ele.me
primary_category: rl
sub_category: uplift-modeling
year: 2025
source_url: https://arxiv.org/abs/2504.18881
tags: [uplift-modeling, merchant-diagnosis, food-delivery, context-aware, two-stage, counterfactual]
---

# TSCAN: Context-Aware Uplift Modeling via Two-Stage Training for Online Merchant Business Diagnosis
**Ele.me** · 2025 · [source](https://arxiv.org/abs/2504.18881)

## Problem
Diagnosing merchant businesses on a food-delivery platform requires estimating individual treatment effects (e.g., of business actions on merchant outcomes), but ITE estimation suffers from sample selection bias. The standard remedies — IPM-based treatment regularization, re-weighting, propensity score modeling — discard information and cap model performance, and existing methods poorly capture how treatment effects shift with external context.

## Approach / System design
TSCAN is a two-stage framework. Stage one (CAN-U) trains with IPM and propensity-score regularization to generate counterfactual uplift labels. Stage two (CAN-D) trains directly on uplift with an isotonic output layer, dropping the regularization components entirely while correcting CAN-U's errors by reinforcing factual samples. A context-aware attention layer runs through both stages, modeling interactions among treatment, merchant features, and external context.

## Key decisions
- Split training into a regularized label-generation stage and a regularization-free direct uplift stage, so the final model avoids the information loss regularization causes.
- Use an isotonic output layer to model uplift directly with monotonic structure.
- Make context a first-class input via attention, since treatment effects vary with external conditions.
- Emphasize factual samples in stage two to adaptively correct stage-one errors.

## Stack
Neural uplift models (CAN-U, CAN-D) with context-aware attention and an isotonic output layer, trained in two stages with counterfactual label generation. Specific serving infrastructure is not covered in the source.

## Results
Validated in extensive experiments on two real-world datasets and through deployment on Ele.me, one of China's largest online food-ordering platforms, for merchant business diagnosis — per the catalog summary, applied across roughly 1 million catering merchants.

## Takeaways
Regularization-based debiasing helps generate counterfactual labels but shouldn't constrain the final model: a two-stage design captures its benefit while shedding its information loss. Context-aware attention is what makes uplift estimates transferable across the varied conditions merchants actually operate in.
