---
id: cs2424
title: "LVMH Data and AI Platform: GenAI for Luxury Client Advisors"
company: LVMH
primary_category: genai
sub_category: agents
year: 2025
source_url: https://cloud.google.com/transform/lvmh-data-ai-platform-interview-franck-le-moal-luxury-gen-ai-louis-vuitton-sephora-dom-perignon
tags: [genai-platform, client-advisor, luxury-retail, vertex-ai, multi-brand, louis-vuitton, sephora]
---

# LVMH Data and AI Platform: GenAI for Luxury Client Advisors
**LVMH** · 2025 · [source](https://cloud.google.com/transform/lvmh-data-ai-platform-interview-franck-le-moal-luxury-gen-ai-louis-vuitton-sephora-dom-perignon)

## Problem
LVMH's 75 brands lacked a unified 360-degree view of customers, making it difficult for client advisors to deliver the hyper-personalized service that defines the luxury experience. Customer data was fragmented across brands, and the conglomerate needed a shared infrastructure that could enable cross-brand analytics without violating per-brand data privacy boundaries.

## Approach / System design
LVMH built a centralized data platform on Google Cloud between 2021 and 2022, with BigQuery as the core component housing customer 360 profiles and product affinity algorithms alongside cross-brand operational benchmarking for finance, HR, and supply chain. Each brand's customer data is firewall-separated so individual maisons maintain autonomy. Generative AI agents for client advisors were layered on top of this foundation using Vertex AI, providing advisors with real-time recommendations and customer context during interactions. The platform philosophy—described internally as "quiet tech"—prioritizes seamless enablement of human relationships over visible automation.

## Key decisions
Building the data foundation before the gen-AI wave (2021–2022) positioned LVMH to adopt Vertex AI agents quickly when generative AI matured, rather than having to retrofit a data platform later. Proprietary product affinity and customer identification algorithms were developed in-house rather than adopting off-the-shelf retail analytics, reflecting the luxury sector's need for brand-differentiated approaches. AI agents are designed to surface insights for advisors rather than replace the advisor relationship, which is central to luxury brand positioning.

## Stack
BigQuery, Vertex AI (Gemini), Google Cloud, custom product affinity algorithms.

## Results
The platform serves over 40,000 users globally per month, processing more than 1.5 million AI queries per month. Operational benefits include improved sales forecasting, better store inventory allocation for high-value items, and accelerated document processing and translation workflows.

## Takeaways
Investing in a shared data platform before AI capabilities are fully mature allows an organization to move quickly when the technology is ready, rather than being blocked by data infrastructure gaps. For conglomerates with many brands, centralizing infrastructure while maintaining strict per-brand data firewalls is the key architectural tension that must be resolved to deliver shared value without brand conflicts.
