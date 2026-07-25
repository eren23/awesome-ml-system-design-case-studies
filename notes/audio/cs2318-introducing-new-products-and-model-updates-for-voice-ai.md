---
id: cs2318
title: Introducing New Products and Model Updates for Voice AI Applications
company: AssemblyAI
primary_category: audio
sub_category: asr
year: 2025
source_url: https://www.assemblyai.com/blog/introducing-new-products-and-model-updates
tags: [asr, speech-to-text, voice-ai, real-time, production-model, universal-3]
---

# Introducing New Products and Model Updates for Voice AI Applications
**AssemblyAI** · 2025 · [source](https://www.assemblyai.com/blog/introducing-new-products-and-model-updates)

## Problem
Teams building production voice AI applications were stitching together fragmented vendors and tools for basic capabilities — language detection, speaker identification, LLM integration — instead of shipping differentiated products. This fragmentation slowed time-to-market and diverted engineering effort away from core product work.

## Approach / System design
AssemblyAI consolidated the voice AI workflow into one platform with three pillars:
- **Speech Understanding**: turns raw transcripts into structured output — speaker identification, custom formatting, translation.
- **Guardrails**: a safety layer over inputs and outputs — profanity filtering, PII redaction, content moderation, plus operational controls like speech thresholds and transcript boundaries.
- **LLM Gateway**: a unified interface that routes transcripts into LLM-powered analysis tasks (with providers like OpenAI GPT and Gemini) without juggling vendors or copying data between systems.

## Key decisions
- Multi-model support with intelligent fallback: Slam (a precision-focused speech language model, in beta) for accuracy-critical work, Universal for broad coverage.
- Integrated prompting so transcript data does not need to be copied across systems for LLM analysis.
- Unified billing across multiple LLM providers behind the gateway.
- Bake safety/operational guardrails into the platform rather than leaving them to each customer.

## Stack
Universal-2 (99-language ASR model with automatic code-switching), Slam speech language AI model (beta), and an LLM gateway routing to models such as GPT and Gemini.

## Results
- 64% reduction in speaker counting errors for audio over 2 minutes.
- 57% accuracy gains on alphanumerics, emails, addresses, and financial terms.
- 45% improvement in domain-specific accuracy using 1,000-word context prompting.
- Customer outcomes: Calabrio reported an 80% satisfaction boost, 22% revenue increase, and 63% developer productivity gain; Siro saw a 90% reduction in support tickets; Delphi cut training-workflow time by 50%; one migration reduced error-handling code by 63%.

## Takeaways
Converging specialized speech models, LLM routing, and operational guardrails behind one API removes non-differentiated integration work for voice AI teams. Speed-to-value and accuracy are complementary when the underlying models are strong across real-world audio conditions.
