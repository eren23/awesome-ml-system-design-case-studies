---
id: cs2264
title: "Slack AI: The Path to Multi-Cloud"
company: Slack
primary_category: mlops
sub_category: platform
year: 2026
source_url: https://slack.engineering/slack-ai-the-path-to-multi-cloud/
tags: [llm-serving, multi-cloud, aws-bedrock, gcp-vertex-ai, inference, high-availability, llmops, provisioned-throughput]
---

# Slack AI: The Path to Multi-Cloud
**Slack** · 2026 · [source](https://slack.engineering/slack-ai-the-path-to-multi-cloud/)

## Problem
Slack had to serve LLMs to millions of enterprise users with strict security, reliability, and latency requirements. A single-cloud, self-managed approach created GPU scarcity, slow scaling, feature lag behind model providers, heavy manual capacity management, and exposure to regional or provider-wide outages.

## Approach / System design
A four-phase evolution (2023–2026):
1. **SageMaker**: self-managed model serving on AWS with a zero-knowledge escrow VPC design for data privacy; manual capacity management became a major engineering drain.
2. **Bedrock**: migration to AWS's managed LLM service for operational simplicity and faster access to new models, using Model Units to abstract throughput.
3. **Bedrock hybrid**: provisioned throughput for latency-sensitive features paired with on-demand capacity for bursty workloads, plus spillover patterns and model hierarchies for automatic failover.
4. **Multi-cloud**: adding GCP Vertex AI as a strategic serving engine (not mere redundancy), behind an intelligent routing layer with circuit breakers and real-time health monitoring.

## Key decisions
- Build an API normalization layer abstracting provider-specific behavior away from application logic.
- Implement a model-hierarchy system for automatic failover across models and providers on performance degradation.
- Route by real-time metrics (latency, quality, error rates) and match features to the specific strengths of individual models.
- Use circuit breakers for automated detection and recovery from endpoint degradation.
- Treat slow responses as failures: monitor soft failures like p90 latency spikes and user-feedback trends, not just hard errors.

## Stack
AWS SageMaker → AWS Bedrock (Provisioned Throughput + On-Demand), GCP Vertex AI, plus custom components: intelligent routing layer, API normalization, circuit breakers, unified monitoring.

## Results
- ~10% quality improvement on complex reasoning tasks and ~67% latency reduction for high-velocity, low-token workloads via feature-to-model matching.
- Zero customer-facing incidents during the Bedrock migration.
- Idle-capacity waste eliminated through demand-responsive routing; model upgrade timelines cut from weeks to days.

## Takeaways
The abstraction layer — not any single provider choice — is the durable competitive asset: it lets Slack adopt breakthroughs quickly and keeps the architecture provider-agnostic. True enterprise-grade reliability requires multi-vendor redundancy, and shipping it at this scale demanded legal, security, compliance, and engineering moving in lockstep.
