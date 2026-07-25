---
id: cs2341
title: "Griffin: How Instacart's ML Platform Tripled ML Applications in a Year"
company: Instacart
primary_category: mlops
sub_category: platform
year: 2023
source_url: https://tech.instacart.com/griffin-how-instacarts-ml-platform-tripled-ml-applications-in-a-year-d3d4dcae3690
tags: [ml-platform, developer-productivity, model-deployment, adoption, standardization]
---

# Griffin: How Instacart's ML Platform Tripled ML Applications in a Year
**Instacart** · 2023 · [source](https://tech.instacart.com/griffin-how-instacarts-ml-platform-tripled-ml-applications-in-a-year-d3d4dcae3690)

## Problem
Instacart's ML footprint spans search over 1B+ products, logistics for 600k+ shoppers, 800+ retailers across 70k+ stores, and 5,000+ brand partners. Its first-generation framework, Lore (open-sourced, started 2016), abstracted data connections and model training well enough for a handful of applications, but its monolithic architecture became a bottleneck as the number, diversity, and complexity of ML applications grew — adding features meant refactoring Lore's core.

## Approach / System design
Griffin is an extensible, self-serve MLOps platform built on a microservice architecture with a hybrid buy-and-build strategy: third-party solutions (Snowflake, AWS, Databricks, Ray) handle specialized workloads, while in-house abstraction layers provide unified access. Four foundational components: MLCLI, an in-house CLI for developing containerized ML applications and managing model lifecycle from templates through notebooks to deployment; Workflow Manager and ML Launcher, which schedule pipelines on Airflow and containerize task execution across compute backends (SageMaker, Databricks, Snowflake) including GPU and high-memory hardware; Feature Marketplace, where features are declared in YAML Feature Definitions, computed via Snowflake/Spark/Flink for batch and real-time, stored across Scylla/Redis/S3 to balance latency and cost, and made discoverable through a UI and RPC service; and a framework-agnostic Training and Inference Platform supporting TensorFlow, PyTorch, Sklearn, XGBoost, FastText, and Faiss, with hyperparameter runs tracked in MLflow and models deployed via Twirp RPC on AWS ECS.

## Key decisions
- Hybrid buy-vs-build: integrate third-party tools behind in-house abstractions so solutions can be swapped with minimal migration overhead.
- Microservices over Lore's monolith for extensibility.
- Docker runtimes everywhere for consistent environments and easier troubleshooting.
- Template-generated code with override ability, letting teams keep legacy systems until they could migrate.
- Regular onboarding codelabs to gather feedback and avoid over-building the "perfect" platform.

## Stack
Snowflake, AWS (ECS, S3), Databricks, Ray, Airflow, Spark, Flink, Scylla, Redis, MLflow, Twirp, Docker; model frameworks TensorFlow, PyTorch, Sklearn, XGBoost, FastText, Faiss.

## Results
The number of ML applications in production tripled within one year of Griffin's rollout, with the platform scaling to hundreds of Airflow DAGs and thousands of tasks in a short period.

## Takeaways
- Careful integration of bought components preserves the ability to switch vendors later.
- Flexibility (custom applications, legacy escape hatches) drives adoption across diverse teams.
- Incremental progress with tight user feedback loops beats years-long pursuit of a perfect platform.
- Extensible, reusable foundations are what allow a small infra team to serve rapid company-wide ML growth.
