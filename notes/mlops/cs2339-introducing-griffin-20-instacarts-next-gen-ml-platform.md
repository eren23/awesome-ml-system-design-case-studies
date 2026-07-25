---
id: cs2339
title: "Introducing Griffin 2.0: Instacart's Next-Gen ML Platform"
company: Instacart
primary_category: mlops
sub_category: platform
year: 2024
source_url: https://tech.instacart.com/introducing-griffin-2-0-instacarts-next-gen-ml-platform-b7331e73b8d7
tags: [ml-platform, model-serving, training-infrastructure, kubernetes, developer-productivity]
---

# Introducing Griffin 2.0: Instacart's Next-Gen ML Platform
**Instacart** · 2024 · [source](https://tech.instacart.com/introducing-griffin-2-0-instacarts-next-gen-ml-platform-b7331e73b8d7)

## Problem
Griffin 1.0 tripled ML applications in a year, but its CLI- and GitHub-PR-based interfaces had a steep learning curve — MLEs took days to weeks to become proficient, needed AWS ECS knowledge to launch inference services, and had to tune system parameters like Gunicorn thread counts outside their domain. Workflows lacked standardization (multiple custom PRs per task, Terraform for inference services), the training platform scaled only vertically (no distributed training or LLM fine-tuning), the MLflow-based model registry couldn't handle hundreds-to-thousands of QPS, third-party integrations fragmented the user experience, and fire-and-forget CLI launches made metadata and training-serving lineage hard to track.

## Approach / System design
Griffin 2.0 consolidates the platform into a service with a web UI. An API Service replaces CLI and PRs with REST APIs (also exposed via a Griffin SDK) for creating features, submitting training jobs, registering models, and standing up inference services; clients like the in-house notebook environment submit jobs programmatically. The ML Training Platform uses Ray for horizontally scaled distributed training, unifies training backends on Kubernetes, and offers configuration-based runtimes for TensorFlow and LightGBM covering data processing, feature transformation, training, evaluation, and batch inference. The ML Serving Platform comprises a Model Registry for artifacts, a Control Plane for UI-driven deployment, a Proxy managing experiments between model versions, and Workers executing feature retrieval, preprocessing, and inference. The Feature Marketplace adds UI-based feature source creation (SQL for batch, Flink SQL/Scala for real-time), data validation to catch generation errors early, and storage optimizations for low-latency access. A unified Griffin UI ties feature definition, workflow management, model registry, and endpoint creation into one place, with validation at each stage.

## Key decisions
- Web UI and REST APIs over CLIs and GitHub PRs to flatten the learning curve.
- One unified platform view integrating external systems (Datadog, MLflow, ECS) instead of tool-hopping.
- Centralized metadata store for the full ML lifecycle, fixing lineage and fire-and-forget gaps.
- Ray plus Kubernetes to make training horizontally scalable and ready for LLM fine-tuning.
- Stage-wise validation to catch errors before jobs consume compute.

## Stack
Ray, Kubernetes, TensorFlow, LightGBM, Flink, MLflow, Datadog, AWS ECS, REST APIs with a Python SDK, in-house notebook environment.

## Results
The serving platform drastically reduced inference service setup time and delivered substantial latency optimization for real-time inference (detailed numbers deferred to the companion serving-platform post). Full realization of the vision was ongoing at publication, with adoption and feedback gathering in progress.

## Takeaways
- Power-user tooling (CLIs, PRs) that worked for early adopters becomes the bottleneck at scale; self-serve UIs unlock the next wave of users.
- Consolidating fragmented vendor integrations behind one platform view pays off in usability and operations.
- Centralized feature/metadata management, distributed computation, and standardized serving position the platform for LLM-era workloads.
