---
id: cs2289
title: Adapting the Facebook Reels RecSys AI Model Based on User Feedback
company: Meta
primary_category: rec
sub_category: feed-ranking
year: 2026
source_url: https://engineering.fb.com/2026/01/14/ml-applications/adapting-the-facebook-reels-recsys-ai-model-based-on-user-feedback/
tags: [reels, user-feedback, survey-model, utis, interest-matching, engagement]
---

# Adapting the Facebook Reels RecSys AI Model Based on User Feedback
**Meta** · 2026 · [source](https://engineering.fb.com/2026/01/14/ml-applications/adapting-the-facebook-reels-recsys-ai-model-based-on-user-feedback/)

## Problem
Facebook Reels ranking leaned on implicit engagement proxies — watch time, likes — which optimize short-term engagement but often miss what users genuinely want to see. The existing approach identified users' true interests with only 48.3% precision, so recommendations drifted from long-term interest alignment.

## Approach / System design
Meta built the User True Interest Survey (UTIS) model: randomized in-feed surveys ask users to rate content relevance on a 1–5 scale, and a lightweight alignment model layer is trained on those responses. UTIS predictions feed two points in the pipeline — as a feature input to late-stage ranking, and in early-stage retrieval to reconstruct user interest profiles. Knowledge distillation aligns sequence-based models with UTIS predictions so the survey signal propagates beyond the alignment layer itself.

## Key decisions
- Binarize survey responses to cut label variance and simplify modeling.
- Weight responses to correct sampling and nonresponse bias in who answers surveys.
- Deploy UTIS as a parallel signal alongside existing engagement models rather than replacing them.
- Design for interpretability so the team can understand which factors drive interest matching.

## Stack
Multi-task, multi-label ranking models; knowledge distillation; large-scale randomized in-feed survey infrastructure; feature engineering over user behavior and content attributes.

## Results
Offline: accuracy 59.5% → 71.5%, precision 48.3% → 63.2%, recall 45.4% → 66.1%. Online A/B tests over 10M+ users: +5.4% high survey ratings, -6.84% low survey ratings, +5.2% total user engagement, and -0.34% integrity violations.

## Takeaways
Directly asking users beats inferring intent from engagement proxies — and the two are complementary: a modest volume of survey labels, carefully debiased and distilled into the ranking stack, moved both satisfaction and engagement. Future directions include better handling of sparse-data users, further debiasing, and LLM-based approaches for diversity.
