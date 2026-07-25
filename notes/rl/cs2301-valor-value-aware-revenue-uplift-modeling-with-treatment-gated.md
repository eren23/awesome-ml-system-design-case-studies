---
id: cs2301
title: "VALOR: Value-Aware Revenue Uplift Modeling with Treatment-Gated Representation for B2B Sales"
company: Google
primary_category: rl
sub_category: uplift-modeling
year: 2026
source_url: https://arxiv.org/abs/2604.02472
tags: [uplift-modeling, b2b-sales, zero-inflated-revenue, causal-inference, treatment-gated]
---

# VALOR: Value-Aware Revenue Uplift Modeling with Treatment-Gated Representation for B2B Sales
**Google** · 2026 · [source](https://arxiv.org/abs/2604.02472)

## Problem
B2B sales teams have scarce human attention and need to spend it on "persuadable" accounts — those whose revenue actually moves when a seller intervenes. Revenue in this setting is zero-inflated (most accounts produce nothing), and standard uplift frameworks break down in two ways: the treatment signal collapses in high-dimensional feature spaces, and objectives calibrated for regression accuracy don't align with correctly ranking the highest-value accounts.

## Approach / System design
VALOR is a unified uplift-modeling framework that pairs a neural network with a gradient-boosted decision tree variant, explicitly optimizing for financial impact rather than raw prediction accuracy. The neural side uses a treatment-gated architecture with bilinear treatment-feature interactions to keep the causal signal from degrading in high dimensions. Training uses a cost-sensitive focal-ZILN (zero-inflated lognormal) objective that combines focal-style robustness to the skewed distribution with value-weighted ranking losses scaled by revenue magnitude. A Robust ZILN-GBDT variant with custom splitting criteria for uplift heterogeneity provides an interpretable counterpart for high-touch sales contexts.

## Key decisions
- Gate representations on treatment (bilinear interactions) instead of concatenating treatment as a plain feature, preserving the causal signal in high-dimensional inputs.
- Optimize a focal-ZILN loss with value-weighted ranking terms so the model prioritizes ranking high-value persuadable accounts, not just fitting the revenue distribution.
- Ship an interpretable tree-based variant alongside the neural model because sales stakeholders need explainable account prioritization.
- Validate with a long-running production A/B test rather than offline metrics alone.

## Stack
Treatment-gated neural network plus a Robust ZILN-GBDT variant; custom focal-ZILN objective for zero-inflated revenue. Specific frameworks/infrastructure are not covered in the source.

## Results
- 20% improvement in rankability over state-of-the-art baselines on public benchmarks.
- 2.7x increase in incremental revenue per account, validated in a 4-month production A/B test.

## Takeaways
For zero-inflated, high-variance business outcomes like B2B revenue, uplift models must be value-aware: preserving the treatment signal architecturally and weighting the loss by financial magnitude beats accuracy-first designs. Pairing a neural model with an interpretable tree variant makes causal targeting usable by human sales teams.
