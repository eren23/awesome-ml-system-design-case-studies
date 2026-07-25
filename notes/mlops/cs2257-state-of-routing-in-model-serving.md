---
id: cs2257
title: State of Routing in Model Serving
company: Netflix
primary_category: mlops
sub_category: efficiency
year: 2026
source_url: https://netflixtechblog.com/state-of-routing-in-model-serving-16e22fe18741
tags: [model-serving, routing, canary-deployment, traffic-splitting, envoy, infrastructure, load-balancing]
---

# State of Routing in Model Serving
**Netflix** · 2026 · [source](https://netflixtechblog.com/state-of-routing-in-model-serving-16e22fe18741)

## Problem
Netflix's centralized model-serving platform must route roughly 1 million requests per second to the right model instance on the right cluster shard, across hundreds of model types and 30+ client microservices, while supporting rapid model iteration, A/B experiments, and traffic splits — all without exposing infrastructure complexity to callers.

## Approach / System design
Two generations of routing:
- **Switchboard**: a custom proxy sitting in the critical path as the mandatory entry point for all model-serving traffic. It performed context-aware routing, experiment allocation, and traffic splitting, configured via JavaScript-based "Switchboard rules" that let researchers define models, A/B tests, and splits without code changes.
- **Lightbulb**: the evolved, decoupled architecture that removes the routing service from the request path. Lightbulb resolves routing metadata and model configuration; the actual request routing is done by Envoy based on headers, with configuration versioned and distributed through Netflix's Gutenberg pub-sub system.

A central abstraction, **Objectives** — domain-agnostic enumerations of business use cases — decouples clients from concrete model implementations, so models can iterate behind a stable interface.

## Key decisions
- Introduce the Objective abstraction so client services never bind to specific models.
- Move from an in-path proxy (Switchboard) to out-of-path configuration resolution (Lightbulb) + Envoy routing, eliminating added latency and the single point of failure.
- Separate model-selection configuration from routing rules so they evolve and fail independently.
- Separate model inputs from request metadata in payloads to cut serialization overhead.

## Stack
Custom Switchboard proxy (1M RPS), Lightbulb configuration-resolution service, Envoy for request routing, Netflix Gutenberg for configuration versioning/distribution, gRPC as the serving protocol.

## Results
Switchboard successfully served 30+ client microservices and hundreds of model types, but added 10–20ms latency per request, posed single-point-of-failure risk, and reduced visibility into traffic origins for training. Lightbulb removed the in-path overhead while keeping the abstraction and experimentation benefits.

## Takeaways
Start centralized to get the abstraction right, then decouple based on operational pain — a staged evolution beat trying to design the perfect system upfront. Treating routing configuration as versioned, distributed infrastructure (not code deployments) accelerated experimentation, and reusing proven components like Envoy cut both build cost and risk.
