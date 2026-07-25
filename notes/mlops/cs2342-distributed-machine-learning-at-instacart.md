---
id: cs2342
title: Distributed Machine Learning at Instacart
company: Instacart
primary_category: mlops
sub_category: platform
year: 2024
source_url: https://tech.instacart.com/distributed-machine-learning-at-instacart-4b11d7569423
tags: [distributed-training, kubernetes, ray, deep-learning, workflow-orchestration]
---

# Distributed Machine Learning at Instacart
**Instacart** · 2024 · [source](https://tech.instacart.com/distributed-machine-learning-at-instacart-4b11d7569423)

## Problem
Instacart's fulfillment ML partitions national data by geography ("zones"), so a single model experiment can launch thousands of parallel training jobs. The legacy Celery-based distributed task queue struggled: workers were over-provisioned to fit the largest models yet ran at 10–15% CPU utilization for lightweight ones, queues sat idle over 60% of the day or backed up with 300–1k+ pending tasks, Python dependencies were shared (and thus hard to upgrade) across all applications on a queue, and the monolithic long-running service was hard to automate or reproduce locally.

## Approach / System design
The team chose Ray as the foundational computation framework and extended Griffin's workflow orchestration for a unified prototyping-to-production experience on Kubernetes. During development, engineers package prototype code and launch it on remote AWS EKS hosts through an internal launcher API wrapping the Ray Job API; the same APIs launch containerized applications to production Ray clusters from Airflow pipelines. Each Ray cluster carries its own Python installation and environment variables, isolating workspaces per application instead of maintaining one monolithic environment. KubeRay provisions, scales, and deletes Ray cluster resources on Kubernetes; applications use Ray Core, Ray AIR, and Ray Serve for distributed patterns. Each fulfillment ML application became an independent, serverless Ray job with a dedicated cluster handling all its zone-level training tasks, replacing the shared long-running queue service.

## Key decisions
- Ray over extending the Celery task-queue architecture, for scalability, resource efficiency, and support for diverse distributed paradigms.
- Serverless per-application Ray jobs instead of shared long-running services.
- Per-cluster environment isolation for independent dependency management.
- Reuse of Griffin's orchestration rather than building a parallel MLOps stack.
- Fine-grained resource sizing: benchmarking showed 2 CPUs per zonal training job sufficed, allowing many more concurrent workers per host.

## Stack
Ray (Core, AIR, Serve, Job API), KubeRay, Kubernetes on AWS EKS, Airflow for production pipelines, Griffin ML platform integration; legacy system was Celery with a message broker/backend.

## Results
For a production fulfillment model running 1.5k unique training tasks on the same 10 16-CPU instances: CPU utilization rose from 10–15% to up to 80%, concurrency went from 10 Celery workers to 70+ Ray workers, and end-to-end completion time dropped from ~4 hours to 20 minutes. Long-running task queue services were deprecated, cutting compute costs. Converting existing training code required only small changes to make functions/classes Ray-remote executable.

## Takeaways
- Monolithic shared compute backends limit scalability, efficiency, and diversity as ML workloads multiply and diverge.
- Serverless, isolated per-application clusters improve execution time, utilization, and developer simplicity simultaneously.
- Even with customizable application topologies, unified build/launch tooling at the platform layer is essential for extensibility.
