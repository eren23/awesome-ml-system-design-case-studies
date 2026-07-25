---
id: cs2092
title: "LLM Assisted Anomaly Detection Service for Site Reliability Engineers: Enhancing Cloud Infrastructure Resilience"
company: IBM
primary_category: anomaly
sub_category: outlier-detection
year: 2025
source_url: https://arxiv.org/abs/2501.16744
tags: [llm, sre, cloud-infrastructure, ibm-cloud, time-series, api-service, grafana]
---

# LLM Assisted Anomaly Detection Service for Site Reliability Engineers: Enhancing Cloud Infrastructure Resilience
**IBM** · 2025 · [source](https://arxiv.org/abs/2501.16744)

## Problem
Site Reliability Engineers monitoring complex cloud infrastructure rely heavily on manual, reactive inspection of time-series telemetry. That approach is slow, delays incident response, and lets problems reach customers. SREs needed a scalable, self-serve way to run anomaly detection over diverse industrial time-series data.

## Approach / System design
IBM built a scalable anomaly detection service exposed through a generalizable API tailored to industrial time-series workloads. The service bundles multiple detection algorithm families — regression-based, mixture-model-based, and semi-supervised — covering both univariate and multivariate series, so users can match technique to data type. A distinguishing addition is an LLM component that models cloud infrastructure components, their failure modes, and expected behaviors, adding semantic understanding on top of the statistical detectors. The manifest notes results surface to SREs through Grafana dashboard integration.

## Key decisions
- API-first design so any SRE team can adopt detection without building their own pipeline.
- Multi-algorithm portfolio rather than a single model, to generalize across heterogeneous time-series data.
- Integrate LLMs for semantic modeling of infrastructure failure modes, not just numeric outlier scoring.
- Roadmap: incorporate time-series foundation models for zero-shot detection.

## Stack
Regression, mixture-model, and semi-supervised detection algorithms; LLM-based infrastructure/failure-mode modeling; service API consumed across IBM cloud operations; Grafana for visualization (per catalog metadata).

## Results
- 500+ active internal users annually.
- ~200,000 API calls in one year.
- Deployed across varied industrial settings, including IoT-based AI applications.
- Detection performance validated on public anomaly benchmarks.

## Takeaways
- Packaging anomaly detection as a shared API service scales far better than per-team tooling — adoption numbers (500+ users, 200K calls/yr) show real pull from SREs.
- No single detector wins everywhere; offering an algorithm portfolio behind one interface is the pragmatic production answer.
- LLMs add value in reliability tooling by encoding what components exist and how they fail, complementing purely statistical detection; foundation models for zero-shot time-series detection are the next step.
