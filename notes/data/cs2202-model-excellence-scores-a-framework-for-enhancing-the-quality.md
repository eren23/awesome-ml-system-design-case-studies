---
id: cs2202
title: "Model Excellence Scores: A Framework for Enhancing the Quality of Machine Learning Systems at Scale"
company: Uber
primary_category: data
sub_category: data-quality
year: 2024
source_url: https://www.uber.com/us/en/blog/enhancing-the-quality-of-machine-learning-systems-at-scale/
tags: [SLO, quality-indicators, quality-objectives, quality-agreements, ml-monitoring, model-lifecycle, measurability]
---

# Model Excellence Scores: A Framework for Enhancing the Quality of Machine Learning Systems at Scale
**Uber** · 2024 · [source](https://www.uber.com/us/en/blog/enhancing-the-quality-of-machine-learning-systems-at-scale/)

## Problem
Uber's ML models drive critical decisions — ride demand prediction, fraud detection, food discovery, ETAs — but teams judged quality almost entirely by offline metrics like AUC and RMSE. Data timeliness, reproducibility, drift, and automated retraining went unmeasured, leaving the organization with poor visibility into ML quality across the model lifecycle.

## Approach / System design
Model Excellence Scores (MES) adapts SLA/SLO thinking from site reliability engineering to ML. Three concepts structure it: Indicators (precise quantitative quality measures), Objectives (target ranges per indicator), and Agreements (indicator collections yielding an overall PASS/FAIL). MES spans four lifecycle phases — prototyping, training, deployment, prediction — with each indicator carrying a defined target range and update frequency. Tracked indicators include data quality (null rates, regional consistency, duplicates), dataset freshness, feature and concept drift, model interpretability, and production prediction accuracy; all normalize to [0,1] or percentages so scores compare across use cases. The framework runs on top of Michelangelo, Uber's ML platform, integrating with existing pipelines, feature stores, model registries, and prediction services.

## Key decisions
Five explicit design principles:
- Automated measurability — every metric quantifiable and computed by infrastructure, no manual scoring.
- Actionability — each indicator has a clear improvement path.
- Aggregatability — scores roll up to org-level OKRs and KPIs.
- Reproducibility — idempotent measurement so values can be backfilled consistently.
- Accountability — every agreement has a named owner.
Also: standardization with flexibility (e.g., ETA models may use MAE where others use RMSE), and incremental rollout prioritizing high-impact models via prioritization matrices rather than boiling the ocean.

## Stack
Michelangelo ML platform plus surrounding infrastructure (data pipelines, feature stores, model registry, distributed training, prediction services); specific tooling beyond the platform is not detailed.

## Results
- 60% improvement in overall model prediction performance after implementation.
- Substantial gains in SLA adherence across quality dimensions; the framework also surfaced needed platform enhancements.

## Takeaways
SLO-style contracts translate well from services to models: making quality measurable and visible motivates practitioners to improve it. Executive buy-in was needed to prioritize quality work against feature work. Automating retraining, revalidation, and redeployment cut maintenance burden and improved freshness, and normalized scores enable apples-to-apples quality conversations across very different models.
