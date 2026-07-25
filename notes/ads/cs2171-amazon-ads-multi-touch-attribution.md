---
id: cs2171
title: Amazon Ads Multi-Touch Attribution
company: Amazon
primary_category: ads
sub_category: attribution
year: 2025
source_url: https://arxiv.org/abs/2508.08209
tags: [multi-touch-attribution, rct, causal-inference, machine-learning, advertising-measurement]
---

# Amazon Ads Multi-Touch Attribution
**Amazon** · 2025 · [source](https://arxiv.org/abs/2508.08209)

## Problem
Advertisers on Amazon need to know how much each ad touchpoint across the marketing funnel actually contributed to a conversion. Assigning credit for a sale across many ad interactions is hard: purely observational ML gives scalable, precise predictions but risks biased estimates of ad effects, while experiments give unbiased effects but are noisy.

## Approach / System design
Amazon Advertising built a production multi-touch attribution (MTA) system that combines randomized controlled trials (RCTs) with ML models. Credit for Amazon conversions is allocated across Amazon Ads touchpoints in proportion to their estimated value, with RCTs anchoring the causal ground truth and ML models providing scale and precision. Amazon shopping signals feed the attribution models.

## Key decisions
- Hybrid RCT + ML methodology instead of choosing either pure experimentation or pure observational modeling.
- Use experiments to correct/validate the bias of observational ML estimates, and ML to smooth the noise of RCTs.
- Ground attribution in proportional value of each touchpoint across the full customer journey rather than last-touch heuristics.

## Stack
Not covered in the source (no specific frameworks or infrastructure named in the abstract).

## Results
Not covered in the source (no quantitative metrics stated in the abstract).

## Takeaways
Principled attribution at scale does not require picking between causal rigor and ML scalability — combining RCTs with ML models yields credit assignment that is both approximately unbiased and operationally deployable across a large ads business.
