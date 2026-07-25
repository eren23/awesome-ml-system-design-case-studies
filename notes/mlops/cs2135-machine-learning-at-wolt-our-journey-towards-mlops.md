---
id: cs2135
title: "Machine learning at Wolt: our journey towards MLOps"
company: Wolt
primary_category: mlops
sub_category: monitoring-infra
year: 2025
source_url: https://careers.wolt.com/en/blog/tech/machine-learning-at-wolt-our-journey-towards-mlops
tags: [mlops, platform, kubernetes, mlflow, model-monitoring, standardization]
---

# Machine learning at Wolt: our journey towards MLOps
**Wolt** · 2025 · [source](https://careers.wolt.com/en/blog/tech/machine-learning-at-wolt-our-journey-towards-mlops)

## Problem
Wolt's data scientists deployed models inconsistently, with no shared infrastructure. Every team reinvented the wheel — custom APIs, monitoring, and logging per model — which blocked central services and made deployment slow and heterogeneous.

## Approach / System design
Wolt built a standardized ML deployment platform on Kubernetes so data scientists can deploy, run, monitor, and maintain models through one path. The effort spanned nearly a year of tool analysis, stakeholder feedback, and iteration. Seldon-Core handles real-time inference deployments, auto-generating REST and gRPC endpoints with built-in monitoring and response logging; MLflow stores model metadata and experiment tracking; training pipelines are Python-based.

## Key decisions
- Seldon-Core as the deployment framework: open source, Kubernetes-native, and compliant with the V2 Data Plane inference API standard.
- Framework agnosticism from day one — XGBoost, scikit-learn, Triton, TensorFlow Serving, and MLflow Server all supported.
- Automatic model updates with performance comparison between versions.
- Standardized deployments to unlock consistent CI patterns across teams.

## Stack
Kubernetes, Seldon-Core, MLflow, Python training pipelines, auto-generated REST/gRPC serving endpoints with built-in monitoring and response logging.

## Results
No quantified metrics in the source; the stated goals were reducing deployment overhead and time-to-production and getting more models into production.

## Takeaways
Treat internal ML teams as customers — stay close to them and optimize their workflow rather than the platform's elegance, and report to stakeholders in terms of what matters to decision-makers instead of behind-the-scenes complexity.
