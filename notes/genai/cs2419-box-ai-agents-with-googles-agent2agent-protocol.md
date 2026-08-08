---
id: cs2419
title: "Box AI Agents with Google's Agent2Agent Protocol"
company: Box
primary_category: genai
sub_category: agents
year: 2025
source_url: https://cloud.google.com/blog/topics/customers/box-ai-agents-with-googles-agent-2-agent-protocol
tags: [a2a-protocol, multi-agent, document-extraction, vertex-ai, agent-interop]
---

# Box AI Agents with Google's Agent2Agent Protocol
**Box** · 2025 · [source](https://cloud.google.com/blog/topics/customers/box-ai-agents-with-googles-agent-2-agent-protocol)

## Problem
Enterprises hold vast quantities of unstructured documents—PDFs, scanned images, contracts, slides—and need to extract structured data from them reliably. Simple extraction is insufficient for business-critical workflows; organizations also need per-field confidence scores to know when to trust AI output and when to route it for human review. Additionally, complex cross-system document workflows require AI agents from different platforms to collaborate securely.

## Approach / System design
Box built an Enhanced Extract AI agent using Google's Agent-2-Agent (A2A) protocol to enable secure interoperability between Box agents and external agents. The agent uses Gemini 2.5 Pro for multimodal document understanding and accesses token-level likelihood data through the A2A connection to construct field-level confidence scores. When extracted values fall below a confidence threshold, the system flags them for human review. Continual learning is supported via in-context learning (corrected examples in prompts) and supervised fine-tuning with LoRA adapters stored per customer, with Gemini's context caching used to reduce inference cost.

## Key decisions
Gemini 2.5 Pro was selected for its combined multimodal comprehension, long-context reasoning, and code generation capabilities, which Box found meaningfully superior to other models for complex document extraction tasks. The A2A protocol was chosen specifically because it exposes token likelihood metadata, enabling confidence scoring that would not be possible through a standard API. LoRA fine-tuning per customer allows the model to adapt to domain-specific document templates without full retraining, while context caching controls inference cost at scale.

## Stack
Gemini 2.5 Pro (Vertex AI), Google Agent Development Kit (ADK), Agent-2-Agent (A2A) protocol, LoRA fine-tuning, Gemini context caching, Google Cloud Marketplace, Agentspace.

## Results
The source reports qualitative improvements in extraction accuracy across PDFs, images, and slides, with per-field confidence scores guiding human review. No specific precision, recall, or throughput numbers are provided.

## Takeaways
Access to token-level model internals through an open inter-agent protocol unlocks uncertainty quantification that standard API calls cannot provide, and confidence-gated human review is a practical way to deploy generative AI safely in business-critical document workflows. Combining LoRA fine-tuning with context caching gives a cost-effective path to customer-specific model adaptation without maintaining separate model deployments per client.
