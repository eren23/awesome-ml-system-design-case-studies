---
id: cs2395
title: How Zendesk ensures you always get the best LLM for the job
company: Zendesk
primary_category: genai
sub_category: agents
year: 2025
source_url: https://www.zendesk.com/blog/product-news/how-zendesk-ensures-you-always-get-the-best-llm-for-the-job/
tags: [llm-routing, multi-model, model-selection, latency, cost-optimization, evaluation, openai, anthropic, gemini]
---

# How Zendesk ensures you always get the best LLM for the job
**Zendesk** · 2025 · [source](https://www.zendesk.com/blog/product-news/how-zendesk-ensures-you-always-get-the-best-llm-for-the-job/)

## Problem
Depending on a single LLM provider risked vendor lock-in, falling behind a fast-moving model landscape, and reliability exposure for enterprise customers — outages or latency spikes at one provider would directly hit Zendesk's AI agent products.

## Approach / System design
Zendesk built a multi-model evaluation and routing platform for its AI agent suite:
- Each AI feature is evaluated across multiple LLM providers, and the model offering the best combination of quality, latency, and cost is selected for that task.
- Multi-homing with automatic failover: if one provider degrades or goes down, traffic shifts to another provider seamlessly.
- The model pool mixes frontier providers (OpenAI, Google, Anthropic, Amazon) with open-source models and Zendesk's own proprietary CX-specialized models trained on customer-experience data.

## Key decisions
- A formal model evaluation framework: offline evaluation, online experiments, and A/B testing gate any model's promotion to production.
- Multi-region deployment across 9+ global regions for data residency compliance and low-latency serving.
- Rigorous vendor onboarding: security vetting, strict data-handling standards, licensing review, and a guarantee that customer data is not reused for model training.
- A modular architecture so models can be swapped or upgraded without disrupting customers.

## Stack
LLM providers: OpenAI, Google, Anthropic, Amazon; open-source models; proprietary Zendesk CX models. Routing, evaluation, and A/B-testing infrastructure built in-house; multi-region serving footprint.

## Results
No specific quantitative performance metrics are disclosed in the post. Zendesk cites its scale of CX domain data (billions of resolutions) as the foundation of its proprietary models.

## Takeaways
- Combining deep domain expertise with whichever frontier model currently leads outperforms committing to any single general-purpose provider.
- Enterprise-grade reliability requires provider redundancy and automatic failover, not just a single-cloud SLA.
- Keeping pace with model releases demands standing evaluation/experimentation infrastructure so swaps are routine rather than projects.
