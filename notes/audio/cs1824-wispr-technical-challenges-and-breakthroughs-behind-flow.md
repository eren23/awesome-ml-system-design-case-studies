---
id: cs1824
title: Wispr — Technical Challenges and Breakthroughs Behind Flow
company: Wispr
primary_category: audio
sub_category: asr
year: 2025
source_url: https://wisprflow.ai/post/technical-challenges
tags: [asr, dictation, low-latency, code-switching, personalization, on-device]
---

# Wispr — Technical Challenges and Breakthroughs Behind Flow
**Wispr** · 2025 · [source](https://wisprflow.ai/post/technical-challenges)

## Problem
Building a voice dictation product that feels effortless demands solving several hard engineering problems simultaneously: ASR and LLM inference that completes in under 200ms, transcription that adapts to context (app, document type, tone), multilingual users who mix languages mid-sentence, and a system that improves from user corrections over time. These requirements span both cloud inference and on-device execution.

## Approach / System design
Wispr's Flow pipeline runs speech recognition followed by an LLM-based formatting and correction stage, both optimized to hit a combined sub-200ms budget. Context-awareness is achieved by feeding the active application or document context into the LLM prompt so that output style and vocabulary are adapted accordingly. Personalization is built from a feedback loop that learns user-specific formatting preferences and vocabulary from corrections. Code-switching is handled at the ASR and post-processing layer to detect and preserve mixed-language utterances.

## Key decisions
Targeting sub-200ms total latency required co-optimizing ASR and LLM serving rather than treating them as independent services. On-device execution was pursued for latency, privacy, and offline use cases. Personalization was treated as a first-class product requirement rather than a post-launch addition.

## Stack
Cloud ASR model, LLM for transcript enhancement and formatting, on-device inference runtime, user correction feedback loop for personalization. Specific framework names are not covered in the source.

## Results
The system achieves sub-200ms combined ASR and LLM inference latency. The dictation experience supports multilingual code-switching and adapts formatting to user preferences over time.

## Takeaways
Voice dictation quality is as much about post-processing intelligence (context-aware formatting, personalization) as it is about raw transcription accuracy. Tight latency budgets require holistic optimization across the full pipeline, and on-device execution can be essential for both latency and privacy goals.
