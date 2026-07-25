---
id: cs2172
title: "On the Factory Floor: ML Engineering for Industrial-Scale Ads Recommendation Models"
company: Google
primary_category: ads
sub_category: ctr-prediction
year: 2022
source_url: https://arxiv.org/abs/2209.05310
tags: [large-scale-ml, ads-recommendation, ctr-prediction, mlops, production-engineering, recsys]
---

# On the Factory Floor: ML Engineering for Industrial-Scale Ads Recommendation Models
**Google** · 2022 · [source](https://arxiv.org/abs/2209.05310)

## Problem
CTR prediction is the central modeling problem for Google's search ads: clicks are the key engagement signal and directly drive advertiser billing under cost-per-click pricing. At industrial scale — a model with billions of parameters trained on 100B+ examples and serving 100k+ QPS — model development is constrained by concerns academic research rarely covers: serving cost, training throughput, and operational reliability.

## Approach / System design
An engineering case study of the practical techniques deployed in Google's production search ads CTR model. The paper frames model quality as one axis among several: efficiency, reproducibility, calibration, and credit attribution are treated as first-class requirements. The model operates under an online learning regime suited to continuously arriving ad data, and the paper describes how candidate ML methods are evaluated for real utility before being adopted at scale.

## Key decisions
- Evaluate new ML techniques against accuracy-per-cost, not accuracy alone — a method must pay for its training/serving footprint.
- Treat reproducibility and calibration as deployment requirements, since billing and auction decisions depend on well-calibrated probabilities.
- Use online learning techniques matched to the non-stationary ads stream.
- Institutionalize a process for deciding which research ideas graduate into the production model.

## Stack
Google's production search ads CTR system. Specific frameworks/hardware are not enumerated in the source abstract.

## Results
Not covered in the source (the abstract states no specific metric improvements). Presented at the ORSUM workshop at ACM RecSys 2022.

## Takeaways
At industrial scale, ML engineering is a discipline of trade-offs: efficiency, reproducibility, calibration, and credit attribution shape which models ship, and the gap between an idea that works in a paper and one that is "useful" in a 100k+ QPS production system is where most of the engineering effort goes.
