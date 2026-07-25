---
id: cs2300
title: "CanniUplift: A Holistic Framework for Mitigating Seller and Incentive Cannibalization in E-commerce Uplift Modeling"
company: Alibaba
primary_category: rl
sub_category: uplift-modeling
year: 2026
source_url: https://arxiv.org/abs/2607.05242
tags: [uplift-modeling, cannibalization, e-commerce, promotions, incremental-gmv, taobao]
---

# CanniUplift: A Holistic Framework for Mitigating Seller and Incentive Cannibalization in E-commerce Uplift Modeling
**Alibaba** · 2026 · [source](https://arxiv.org/abs/2607.05242)

## Problem
Uplift models estimating individual treatment effects for personalized incentive allocation assume SUTVA, which breaks in a multi-seller marketplace. Two forms of value leakage result: seller-level cannibalization, where a coupon merely shifts a customer's spend from one shop to another without growing platform GMV, and incentive-level cannibalization, where organic conversions and alternative rewards pollute treatment-effect attribution. Standard uplift models credit incentives with revenue they didn't actually create.

## Approach / System design
Taobao & Tmall Group's CanniUplift framework has three components: Platform-level Global Alignment (PGA), which imposes global GMV consistency constraints to capture cross-shop substitution and detect when incentives cannibalize rather than create value; Redemption-based Decomposition Denoising (RDD), which uses coupon-redemption behavior to decompose outcomes and strip attribution noise within an entire-space modeling framework; and a Treat-Attention mechanism modeling interactions between user historical behavior and the treatment options.

## Key decisions
- Model cannibalization explicitly at the platform level instead of assuming per-shop treatment effects are independent.
- Anchor denoising in observed redemption behavior rather than heuristics about organic conversion.
- Optimize for platform-wide incremental GMV, not per-seller or per-coupon lift.

## Stack
Neural uplift modeling with attention over user behavior and treatments, entire-space decomposition, and global-consistency constraints. Specific infrastructure is not covered in the source.

## Results
Online A/B tests against the production baseline showed a 4.08% relative increase in incremental GMV with improved ROI. Ablations confirmed that integrating PGA and RDD consistently improves wAUUC and wQINI offline metrics.

## Takeaways
In multi-seller marketplaces, naive uplift modeling systematically over-credits incentives; explicitly modeling cross-shop substitution and redemption-based attribution converts that leakage into measurable incremental value. Platform-level consistency constraints are a practical way to inject the marketplace-wide view into per-user treatment models.
