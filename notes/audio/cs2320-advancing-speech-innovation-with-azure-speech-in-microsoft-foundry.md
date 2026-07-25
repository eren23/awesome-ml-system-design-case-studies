---
id: cs2320
title: Advancing Speech Innovation with Azure Speech in Microsoft Foundry
company: Microsoft
primary_category: audio
sub_category: asr
year: 2025
source_url: https://techcommunity.microsoft.com/blog/azure-ai-foundry-blog/advancing-speech-innovation-with-azure-speech-in-microsoft-foundry/4471461
tags: [voice-ai, speech-to-speech, voice-live-api, azure, genai, real-time, production]
---

# Advancing Speech Innovation with Azure Speech in Microsoft Foundry
**Microsoft** · 2025 · [source](https://techcommunity.microsoft.com/blog/azure-ai-foundry-blog/advancing-speech-innovation-with-azure-speech-in-microsoft-foundry/4471461)

## Problem
Voice is becoming the primary interface between people and AI, but building production voice agents has historically required stitching together separate ASR, LLM, and TTS components, plus custom logic for turn-taking, latency, and branding. Enterprises wanted a single path to voice-enable agents for scenarios like customer service, in-car assistants, e-learning, and employee support without deep speech-AI expertise on every product team.

## Approach / System design
Announced at Microsoft Ignite 2025 as a wave of Azure Speech capabilities inside Microsoft Foundry:
- **Voice Live API (GA)**: a unified single API for real-time speech-to-speech conversation, combining speech input, GenAI reasoning, and natural speech output. Developers pick from 10+ natively integrated foundation GenAI models (including GPT-Realtime and GPT-Realtime-Mini) or bring their own model deployed in Foundry. Speech input covers 140+ locales; hundreds of multilingual neural voices (including HD V2) span 150+ locales. Azure semantic VAD improves detection of user speech activity for natural turn-taking; custom speech, custom voice, and custom avatars support branded agents.
- **Live Interpreter API (GA)**: real-time speech-to-speech translation using the same underlying model that powers Microsoft Teams' Live Interpreter, with continuous automatic language detection across all 76 input languages supported by Azure Speech, 9 output languages at launch, ultra-low latency near human parity, and personal voice that preserves the original speaker's tone and style.
- **LLM Speech API (public preview)**: LLM-powered transcription and translation of audio files with contextual understanding, prompt tuning of output text, speaker diarization, word timing, multi-channel support, and fast inference — aimed at meeting notes, agent assist, voicemail, and caption generation.
- **Photo Avatar (public preview)**: powered by Microsoft Research's VASA-1 model, generates an expressive head-only talking avatar instantly from a single image (30 standard avatars out of the box, plus custom branded ones), avoiding the video shoots and model training that video avatars require.
- **Developer experience**: Azure Speech APIs (Speech to Text, Text to Speech, Avatar, Voice Live) deployable from the Foundry model catalog, and an Azure Speech MCP Server in the Foundry Tools catalog to expose speech capabilities as agent tools.

## Key decisions
- Collapse the ASR → LLM → TTS pipeline into one managed real-time API rather than requiring developers to orchestrate components themselves.
- Support both built-in GenAI models and bring-your-own Foundry model deployments to avoid locking customers into a single model family.
- Reuse the production-proven Teams interpreter model as a public API rather than building a separate translation stack.
- Offer single-photo avatar generation as a lightweight alternative to full video-avatar training.
- Expose speech as MCP tools so agent builders can compose voice capabilities like any other tool.

## Stack
Azure Speech, Microsoft Foundry (model catalog, Tools catalog), Voice Live API, Live Interpreter API, LLM Speech API, GPT-Realtime / GPT-Realtime-Mini, VASA-1 (Photo Avatar), Azure semantic VAD, custom voice/custom avatar, Azure Speech MCP Server, Azure Communication Services (in the eClinicalWorks deployment).

## Results
- Voice Live API evaluated by thousands of customers during public preview across customer service, in-car, public service, e-learning, and support-agent scenarios.
- eClinicalWorks' healow Genie contact center uses Voice Live plus Azure Communication Services to automate routine patient calls; Capgemini reports measurable improvements in user engagement and satisfaction from low-latency voice interactions in its global service desk operations; Astra Tech's botim platform uses it as a standardized voice framework so product teams don't need dedicated AI hires; Gulf Air uses photo avatars in crew training; Oppo and Caption Connect are testing Live Interpreter; Anker uses LLM Speech.
- No aggregate quantitative benchmarks were published in the post.

## Takeaways
- Real-time speech-to-speech is being packaged as a single production API surface, shifting the integration burden from app teams to the platform.
- Preserving speaker identity (personal voice) and natural turn-taking (semantic VAD) are treated as first-class product features, not add-ons.
- Enterprise adoption stories emphasize standardization: one voice framework that many internal teams can reuse without speech expertise.
