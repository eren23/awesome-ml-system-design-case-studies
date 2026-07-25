---
id: cs2127
title: "Klarna AI Assistant: Handling 2.3M Customer Conversations"
company: Klarna
primary_category: genai
sub_category: rag
year: 2025
source_url: https://openai.com/index/klarna/
tags: [customer-service, gpt-4, multi-language, api-integration, deflection, rag, resolution-time]
---

# Klarna AI Assistant: Handling 2.3M Customer Conversations
**Klarna** · 2025 · [source](https://openai.com/index/klarna/)

## Problem
Klarna serves 150 million consumers globally and faced heavy customer-service volume alongside a tedious product search and comparison experience for shoppers. It needed AI that could resolve support conversations at scale across many languages and markets without degrading service quality.

## Approach / System design
Klarna deployed two complementary OpenAI-powered systems: a customer-facing AI assistant embedded in existing customer-service workflows (plus a ChatGPT plugin for conversational shopping with product recommendations and price comparisons), and ChatGPT Enterprise rolled out internally to augment employee productivity. The assistant runs 24/7 with multilingual support spanning Klarna's distributed markets.

## Key decisions
- Build on OpenAI's GPT-4-class models for both the consumer assistant and internal enterprise tooling.
- Integrate the assistant into existing customer-service workflows rather than replacing them, escalating to humans where needed.
- Design for multi-language coverage from the start: 35+ languages across 23 markets.

## Stack
OpenAI GPT models via the ChatGPT plugin ecosystem and ChatGPT Enterprise; integration with Klarna's customer-service platform. Deeper architecture details are not covered in the source.

## Results
In its first month the assistant handled 2.3 million conversations — two-thirds of all customer-service chats, equivalent to the work of 700 full-time agents. Customer satisfaction was on par with human agents, repeat inquiries dropped 25%, and average resolution time fell from 11 minutes to under 2 minutes. Klarna projected a $40 million profit improvement for 2024, and 90% of employees adopted generative AI tools daily.

## Takeaways
Pairing a customer-facing assistant with organization-wide internal AI adoption produced compounding gains: large support deflection with quality parity, faster resolutions, and a workforce refocused on complex cases.
