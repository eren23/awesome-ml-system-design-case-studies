---
id: cs2134
title: "Grab AI Gateway: Connecting Grabbers to multiple GenAI providers"
company: Grab
primary_category: mlops
sub_category: efficiency
year: 2025
source_url: https://engineering.grab.com/grab-ai-gateway
tags: [genai, llm-gateway, multi-provider, rate-limiting, pii-redaction]
---

# Grab AI Gateway: Connecting Grabbers to multiple GenAI providers
**Grab** · 2025 · [source](https://engineering.grab.com/grab-ai-gateway)

## Problem
Grab teams needed access to multiple GenAI providers (OpenAI, Azure, AWS Bedrock, Google Vertex AI), but direct integration meant fragmented authentication, no unified cost control, security/compliance gaps, and duplicated effort across the organization.

## Approach / System design
The AI Gateway is a lightweight reverse proxy between internal users and external providers, deliberately minimalist — it intervenes only when necessary, handling authentication, authorization, and rate limiting without heavy request processing. It offers a unified OpenAI-compatible API schema translated to each provider's format, dynamic routing across reserved instances and regions to maximize quota utilization, and identity/access management with short-term exploration keys and long-term production keys under path-based authorization. All requests and responses are logged to the data lake for auditing, with request-level cost attribution (separate jobs handle async costs like fine-tuning).

## Key decisions
- Reverse-proxy design for out-of-the-box SDK compatibility, accepting edge cases that require ongoing integration testing.
- Minimalist scope so the platform can keep pace with rapid provider innovation without ballooning operational burden.
- Centralized audit logging and per-request cost attribution for compliance and fair chargeback.
- Platform integrations (automatic key provisioning in Chimera notebooks, Catwalk deployment) to lower adoption friction.

## Stack
Reverse proxies fronting OpenAI, Azure, AWS Bedrock, and Google Vertex AI; Chimera notebooks for development; Catwalk ML platform for deployment; vLLM for open-source model serving; data lake for audit trails and analytics.

## Results
300+ unique use cases onboarded since 2023, 3,000+ Grabbers with exploration keys, and 50+ supported AI models, powering production applications such as real-time audio analysis, content moderation, and menu description generation.

## Takeaways
A thin, centralized gateway buys cost visibility, security, and fair resource allocation across batch and online SLOs without slowing teams down. Next steps include model cataloging, built-in governance/guardrails, and token/cost-based rate limiting beyond simple request counts.
