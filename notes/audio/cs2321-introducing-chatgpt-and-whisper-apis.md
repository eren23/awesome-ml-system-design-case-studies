---
id: cs2321
title: Introducing ChatGPT and Whisper APIs
company: OpenAI
primary_category: audio
sub_category: asr
year: 2023
source_url: https://openai.com/index/introducing-chatgpt-and-whisper-apis/
tags: [asr, whisper, speech-to-text, api, commercial-deployment, production, multilingual]
---

# Introducing ChatGPT and Whisper APIs
**OpenAI** · 2023 · [source](https://openai.com/index/introducing-chatgpt-and-whisper-apis/)

## Problem
Whisper, open-sourced in September 2022, was widely praised but hard for many teams to run and scale themselves; ChatGPT-class language capability was similarly locked inside the consumer product. OpenAI needed to turn both into reliable, cheap, production API services that third-party developers could build on.

## Approach / System design
- **ChatGPT API**: released `gpt-3.5-turbo`, the same model behind the ChatGPT product, at $0.002 per 1K tokens — 10x cheaper than existing GPT-3.5 models. A series of system-wide optimizations cut ChatGPT serving costs by 90% since December, and those savings were passed through to API pricing.
- **Chat-native interface**: instead of raw text completion, the new `/v1/chat/completions` endpoint consumes a sequence of role-tagged messages plus metadata; under the hood the input is rendered to tokens via a new format, Chat Markup Language (ChatML).
- **Model versioning**: `gpt-3.5-turbo` tracks the recommended stable model, while pinned snapshots (e.g. `gpt-3.5-turbo-0301`) give developers version stability with published support windows.
- **Dedicated instances**: for heavy users, compute can be reserved by time period on OpenAI's Azure-based infrastructure instead of pay-per-request shared capacity, with control over instance load, longer context limits, and model-snapshot pinning; economical beyond roughly 450M tokens/day.
- **Whisper API**: the open-source `large-v2` model served through transcription (source-language) and translation (to-English) endpoints at $0.006/minute, accepting m4a, mp3, mp4, mpeg, mpga, wav, and webm, with a highly optimized serving stack for faster performance than self-hosting or other services.
- **Developer terms**: API data no longer used for training by default (opt-in only), default 30-day retention, pre-launch review removed in favor of automated monitoring, and users own model inputs and outputs.

## Key decisions
- Aggressively price both APIs by first driving down inference cost (90% reduction) rather than premium-pricing frontier capability.
- Introduce a structured chat message format (ChatML) as the API abstraction instead of raw prompt strings.
- Offer the same open-source Whisper weights as a managed service, competing on serving performance and convenience rather than model exclusivity.
- Give large customers dedicated capacity to optimize workloads against hardware directly.
- Change data-usage defaults (no training on API data) to unblock enterprise adoption.

## Stack
gpt-3.5-turbo, Whisper large-v2 (`whisper-1`), ChatML, REST API with Python bindings, Azure compute infrastructure, dedicated instance provisioning.

## Results
- ChatGPT serving cost reduced 90% since December 2022; API priced at $0.002/1K tokens; Whisper at $0.006/minute.
- Early production adopters: Snap's My AI for Snapchat+ (750M monthly Snapchatters), Quizlet's Q-Chat tutor (60M+ students), Instacart's "Ask Instacart" shoppable answers (75,000+ retail partner locations), Shopify's Shop assistant (100M shoppers), and Speak's AI speaking companion (fastest-growing English-learning app in South Korea, built on the Whisper API).
- OpenAI acknowledged uptime had fallen short for two months and made production stability the engineering team's top priority.

## Takeaways
- Commodity-priced APIs, not model releases, were the unlock for a wave of consumer-scale AI integrations.
- Serving-stack optimization is a competitive product lever: the same open-source model can win as a paid API on speed and convenience.
- Data-retention and training-usage defaults are adoption blockers for enterprises and were explicitly reversed here.
- Version pinning and dedicated capacity are the mechanisms that make a continuously improving model consumable by production systems.
