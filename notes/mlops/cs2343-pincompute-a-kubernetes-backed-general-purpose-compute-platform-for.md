---
id: cs2343
title: "PinCompute: A Kubernetes Backed General Purpose Compute Platform for Pinterest"
company: Pinterest
primary_category: mlops
sub_category: platform
year: 2024
source_url: https://medium.com/pinterest-engineering/pincompute-a-kubernetes-backed-general-purpose-compute-platform-for-pinterest-8ad408df2d6f
tags: [compute-platform, kubernetes, ml-infrastructure, resource-management, general-purpose]
---

# PinCompute: A Kubernetes Backed General Purpose Compute Platform for Pinterest
**Pinterest** · 2024 · [source](https://medium.com/pinterest-engineering/pincompute-a-kubernetes-backed-general-purpose-compute-platform-for-pinterest-8ad408df2d6f)

## Problem
Pinterest teams were spending effort on undifferentiated infrastructure management — provisioning, Kubernetes operations, OS upgrades, sidecar rollouts — instead of application logic. Pinterest wanted an application-centric, fully managed compute API covering the 90th percentile of use cases, spanning long-running services, run-to-finish jobs, ML training, scheduled jobs, and infrastructure services, while driving down infrastructure cost.

## Approach / System design
PinCompute is a regional multi-tenant PaaS on Kubernetes with a federated architecture: a host cluster runs the regional federation control plane (quota enforcement, workload sharding, member cluster selection, status aggregation), while zonal member clusters — aligned with cloud provider failure domains — execute workloads via in-house and open-source operators. Workloads are defined as Custom Resources. New primitives: PinPod, a Pod-like building block with per-container updates, managed sidecars, data persistence, and failovers; PinApp for long-running applications with zone-based rollouts and zonal capacity balancing; and PinScaler for autoscaling integrated with Statsboard metrics (CPU/memory, scheduled, and custom metrics, with cooldowns and min/max guards). Run-to-finish work uses PinterestJobSet, PinterestTrainingJob (Kubeflow TFJob/PyTorchJob), and PinterestCronJob; infrastructure services deploy as PinterestDaemons or a proprietary PinterestSideCar. Access goes through PinCompute APIs (workload, operation, insight) with a caching layer offloading Kubernetes API reads, rate limiting, integrated authn/authz/audit, simplified data models (dropping managed fields cuts API payloads up to 50%), and a versioned SDK encapsulating retries, backoff, and metrics. Scheduling is two-level: cluster-level filtering/scoring in the federation plane, then a Kubernetes scheduler-framework-based Pod scheduler in member clusters. Resources come in Reserved, OnDemand, and (in development) Preemptible tiers. Node runtime provides isolated tenancy per Pod, a proprietary networking plugin (bridge port, routable IP, dedicated ENI), volume plugins including logging integration, health probing as a readiness gate, and automatic remediation with rate limiting and circuit breaking. Automated, application-aware cluster rotation and a four-stage release pipeline with a continuously running end-to-end canary framework manage platform changes.

## Key decisions
- Federation of many zonal Kubernetes clusters rather than one giant cluster, bounding blast radius and enabling horizontal scale-out.
- Purpose-built primitives (PinPod/PinApp/PinScaler) over raw Kubernetes objects, separating application from infrastructure concerns (e.g., per-container updates avoid disturbing user containers during sidecar upgrades).
- A gateway API with simplified semantics instead of exposing raw Kubernetes APIs.
- Resource tiering plus multi-tenancy, oversubscription, and bin packing for cost efficiency; GPU migration from P4 to G5 instance families.
- Decoupled debugging via node-level APIs (container shells, live log streaming) off the critical Kubernetes control path.

## Stack
Kubernetes (federated host/member clusters), Custom Resources and operators, Kubeflow training operators, Kubernetes scheduler framework with proprietary plugins, proprietary networking and volume plugins, Statsboard, OpenAPI-generated clients/SDKs, AWS instance families including Graviton and G5 GPUs.

## Results
Each cluster is optimized for a sweet spot of 3,000 nodes, 120k pods, and 1,000 mutating pod operations per minute with 25s P99 end-to-end workload launch latency; the platform scales horizontally by adding member clusters. SLOs include 99.9% availability on critical workload orchestration APIs and reconcile-latency targets from seconds to tens of seconds. GPU cost was reduced while capacity grew to support the business. Internal research found >90% of use cases with >60% of infrastructure footprint can benefit from the PaaS.

## Takeaways
- PaaS abstraction was the biggest win for developers, and standardization gave operators leverage on efficiency and upgrades.
- "API First" makes the platform programmable and extendable with a crisp support contract.
- A solid definition of tenancy is critical for multi-tenant platforms.
- Doubling down on automation (remediation, rotation, releases) cut support response time and on-call overhead.
