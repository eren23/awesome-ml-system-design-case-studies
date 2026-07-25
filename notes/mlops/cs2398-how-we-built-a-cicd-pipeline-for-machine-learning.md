---
id: cs2398
title: How we built a CI/CD Pipeline for machine learning with online training in Kubeflow
company: Itaú Unibanco
primary_category: mlops
sub_category: training-infra
year: 2019
source_url: https://cloud.google.com/blog/products/ai-machine-learning/itau-unibanco-how-we-built-a-cicd-pipeline-for-machine-learning-with-online-training-in-kubeflow
tags: [kubeflow, cicd, ml pipeline, kubernetes, online training, model deployment, nlp, chatbot]
---

# How we built a CI/CD Pipeline for machine learning with online training in Kubeflow
**Itaú Unibanco** · 2019 · [source](https://cloud.google.com/blog/products/ai-machine-learning/itau-unibanco-how-we-built-a-cicd-pipeline-for-machine-learning-with-online-training-in-kubeflow)

## Problem
Itaú's virtual assistant AVI serves roughly 1M customers a month at 85% accuracy, but getting a new or retrained model into production took up to a week of manual steps and change-management procedures. The bank needed to run multiple models/techniques in parallel in production, retrain on fresh data in the production environment, automatically promote new techniques, and support A/B testing with simultaneously served models.

## Approach / System design
An end-to-end CI/CD pipeline: source code in Git → Jenkins CI build → container registry → Kubeflow Pipelines training run → model artifact in Cloud Storage → Seldon Core serving behind REST endpoints. A standardized repo convention (Dockerfile, trainer entrypoint, model source, KFP pipeline definition) makes every model plug into the same pipeline. The KFP pipeline uses three containers: a trainer (scikit-learn + Spacy text models), a serving deployer, and a generic "pkl server" Seldon container that downloads the trained artifact from Cloud Storage and exposes a `predict()` REST API. Retraining can be triggered at runtime from an admin UI via the Kubeflow Pipelines REST API.

## Key decisions
- Open-source, portable tooling (Kubeflow, Kubernetes, Docker, Git) so the same pipeline runs on GCP (GKE) and on-premises (OpenShift Origin) — a deliberate hybrid/multi-cloud hedge.
- Convention over configuration: a fixed repository structure and naming scheme to manage many models uniformly.
- A generic serving container decoupled from any specific model, so deployment infrastructure never changes per model.
- API-driven pipeline runs, letting business applications and admin tooling trigger online retraining.
- Versioned model paths in Cloud Storage enabling multiple simultaneous model versions for A/B tests and gradual rollouts.

## Stack
GitLab, Jenkins, Docker, Google Container Registry, Kubernetes (GKE and OpenShift), Kubeflow Pipelines, Seldon Core, Google Cloud Storage, scikit-learn, Spacy.

## Results
- Model training-and-deployment cycle cut from about one week to hours.
- AVI operates at 85% customer-service accuracy and a 98% question-handling success rate for ~1M monthly users.
- The platform was assembled with very little custom development by composing mature open-source components.

## Takeaways
- Automating the train→deploy path is what unlocks iteration speed; the models themselves didn't need to change.
- Standardized repo conventions plus a generic serving container scale to many models with near-zero per-model infrastructure work.
- Choosing portable open-source building blocks preserved deployment flexibility across cloud and on-prem — important in a regulated banking environment.
