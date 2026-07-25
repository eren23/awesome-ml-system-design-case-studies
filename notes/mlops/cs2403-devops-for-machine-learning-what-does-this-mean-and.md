---
id: cs2403
title: DevOps for Machine Learning – What does this mean, and why do you need it?
company: Delivery Hero
primary_category: mlops
sub_category: monitoring-infra
year: 2021
source_url: https://tech.deliveryhero.com/devops-for-machine-learning-what-does-this-mean-and-why-do-you-need-it/
tags: [devops, mlops, ml practices, cicd, model deployment, scalability, automation]
---

# DevOps for Machine Learning – What does this mean, and why do you need it?
**Delivery Hero** · 2021 · [source](https://tech.deliveryhero.com/devops-for-machine-learning-what-does-this-mean-and-why-do-you-need-it/)

## Problem
Classic DevOps assumes data is ephemeral and stays in sync with software versions. ML breaks that assumption: datasets evolve on their own rhythm, models carry complex dependencies, and the AI component itself is a "gray/black box" that is costly to produce, opaque, and hard to reproduce exactly. At Delivery Hero's scale — more than 10M orders a day across 30+ countries — this misalignment between fast software deployment and the data/model lifecycle becomes a real operational risk.

## Approach / System design
Extend DevOps principles so that data and ML artifacts are first-class citizens with their own governance, alongside the usual infrastructure and application concerns. The post frames MLOps as DevOps plus dedicated practices for the data/model lifecycle rather than a separate discipline.

## Key decisions
- Add new practice areas that classic DevOps lacks: data generation, data testing, data versioning, and automation of the data/model lifecycle.
- Upgrade existing practices for ML: production-replica testing environments, precise documentation of business processes, data lineage tracking, and cross-organizational visibility of data flows.
- Treat the ML component as a major source of cost and unpredictability that must be explicitly managed, not hidden behind service boundaries.

## Stack
Not covered in the source — the article is conceptual/strategic and does not prescribe specific tools.

## Results
No quantitative before/after results are given; the article motivates the practice with Delivery Hero's operating scale (10M+ daily orders, 30+ countries) rather than measured MLOps impact.

## Takeaways
- ML amplifies DevOps complexity because models are expensive to build, opaque, and imperfectly reproducible.
- Data-centric practices (testing, versioning, lineage) are where most organizations have the largest maturity gap.
- Applying DevOps discipline to data and models is a prerequisite for shipping and maintaining ML reliably at multi-country scale.
