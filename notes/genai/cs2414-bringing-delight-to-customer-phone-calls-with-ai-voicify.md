---
id: cs2414
title: Bringing Delight to Customer Phone Calls with AI (Voicify)
company: Voicify
primary_category: genai
sub_category: chatbots
year: 2026
source_url: https://cloud.google.com/blog/topics/customers/bringing-delight-to-customer-phone-calls-with-ai
tags: [voice-ai, conversational-ai, google-cloud, dialogflow, restaurant-ordering]
---

# Bringing Delight to Customer Phone Calls with AI (Voicify)
**Voicify** · 2026 · [source](https://cloud.google.com/blog/topics/customers/bringing-delight-to-customer-phone-calls-with-ai)

## Problem
Restaurants were losing roughly 20% of incoming calls and orders due to unattended phones, while healthcare providers struggled with high call volumes demanding near-perfect accuracy for appointment scheduling. Building voice AI for these industries requires handling transactional precision, extreme traffic spikes (e.g., day before Thanksgiving), sub-second latency, and strict compliance requirements including HIPAA, SOC2, ISO27001, and PCI.

## Approach / System design
Voicify built a voice orchestration platform that chains ASR, text generation (a mix of generative and programmatic logic), and TTS into a single customer call pipeline. Gemini Flash serves as the core language model, running on Vertex AI (upgraded from Google AI Studio) to satisfy enterprise uptime and compliance guarantees. Rather than injecting full restaurant menus into prompts, the system progressively retrieves only the relevant menu portion as the conversation advances, reducing prompt size and latency.

## Key decisions
Moving from Google AI Studio to Vertex AI and then to the Gemini Enterprise Agent Platform provided the reliability and security guarantees required for healthcare clients. Capacity is managed through a combination of provisioned throughput and premium pay-as-you-go, allowing the platform to absorb sudden demand spikes without rate limiting. The decision to do partial menu injection rather than full context stuffing measurably improved time-to-first-token.

## Stack
Gemini Flash (LLM), Vertex AI / Gemini Enterprise Agent Platform, custom voice orchestration layer with ASR and TTS components, POS and practice-management system integrations, multicloud deployment.

## Results
Voicify achieved 25–30% cost savings compared to previous LLM providers while maintaining 100% uptime with no dropped responses during peak events. New restaurant clients can be onboarded in 1–2 days, down from 1–2 weeks prior to the platform migration.

## Takeaways
Minimizing time-to-first-token is critical for voice AI because even short pauses cause callers to hang up. A hybrid capacity model — provisioned throughput supplemented by on-demand pay-as-you-go — is more cost-effective than pure provisioned capacity for workloads with sharp, predictable spikes. Enterprise compliance requirements (HIPAA, SOC2) must be architected from the start rather than retrofitted, and choosing an enterprise-grade AI platform substantially reduces the operational burden of meeting them.
