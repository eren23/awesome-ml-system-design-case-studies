---
id: cs2402
title: "Railyard: how we rapidly train machine learning models with Kubernetes"
company: Stripe
primary_category: mlops
sub_category: platform
year: 2021
source_url: https://stripe.com/blog/railyard-training-models
tags: [training infrastructure, kubernetes, ml platform, model training, job scheduling, hyperparameter tuning, distributed training]
---

# Railyard: how we rapidly train machine learning models with Kubernetes
**Stripe** · 2021 · [source](https://stripe.com/blog/railyard-training-models)

## Problem
Stripe's model training had outgrown ad hoc manual runs on EC2 instances. The company needed to support hundreds of daily training jobs across diverse frameworks (scikit-learn, XGBoost, PyTorch, FastText), track model state, ownership, and provenance centrally, and match jobs with very different compute profiles (CPU, GPU, memory-intensive) to appropriate hardware.

## Approach / System design
Railyard is a Scala API service running on Kubernetes that manages the training-job lifecycle: a JSON API accepts job submissions; Postgres stores job state, history, and model provenance; Kubernetes executes and schedules the containerized jobs; S3 holds logs and training outputs. Users describe data sources, filters, features, and hyperparameters in the API request, and implement the actual training logic in Python via a `StripeMLWorkflow` class with a `train()` method. Standardized data interfaces (Pandas DataFrames, PyTorch Datasets) keep workflows consistent while leaving modeling code free-form.

## Key decisions
- API design: no framework-specific DSL — core training logic lives entirely in Python, with a free-form `custom_params` JSON field for needs the API didn't anticipate.
- Packaging: Python workflows built with Bazel and Google's Subpar into standalone executables, containerized and pushed to AWS ECR.
- Instance pairing: jobs declare compute requirements and Kubernetes affinity/toleration rules route them — big jobs get dedicated nodes, small jobs pack together on shared ones.
- A dedicated team runs the Kubernetes cluster, so ML teams never touch cluster operations.
- Training-as-an-API enables orchestration from schedulers like Airflow.

## Stack
Scala (API service), Python (workflows), Kubernetes, Postgres, S3, AWS ECR, Bazel + Subpar, scikit-learn, XGBoost, PyTorch, FastText.

## Results
- Nearly 100,000 models trained on Kubernetes in the first 1.5 years, with hundreds of new models trained daily.
- Models built on roughly billions of data points serve hundreds of millions of predictions.
- Centralized job state moved support from reactive debugging ("my model didn't train") to proactive, metrics-driven operations.

## Takeaways
- A framework-agnostic API lets teams adopt new ML libraries without any infrastructure change.
- Declaring resource needs and letting the scheduler pair jobs to instance types beats hand-picking machines.
- Memory-intensive workflows remain the hard edge; the team was eyeing distributed libraries like dask-ml as the next step.
