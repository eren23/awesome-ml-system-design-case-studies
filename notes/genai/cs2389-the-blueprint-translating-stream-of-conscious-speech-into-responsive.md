---
id: cs2389
title: "The Blueprint: Translating stream-of-conscious speech into responsive, actionable task lists"
company: Doist
primary_category: genai
sub_category: agents
year: 2026
source_url: https://cloud.google.com/blog/topics/startups/the-blueprint-doist-stream-of-consciousness-ai-task-list-creation
tags: [voice-ai, streaming, gemini, task-management, live-api, tool-calling, multilingual]
---

# The Blueprint: Translating stream-of-conscious speech into responsive, actionable task lists
**Doist** · 2026 · [source](https://cloud.google.com/blog/topics/startups/the-blueprint-doist-stream-of-consciousness-ai-task-list-creation)

## Problem
Doist wanted Todoist users to talk in an unstructured stream of consciousness and get back a clean, actionable task list (Ramble). Four hard problems: fast, accurate real-time interaction with tool calling; multilingual speech with slang and accents; testing non-deterministic output for semantic correctness; and reliable audio capture across browsers and mobile contexts.

## Approach / System design
Ramble is built on the Gemini Live API with Gemini Flash models via the Gemini Enterprise Agent Platform. The backend is provider-agnostic and modular: a streaming layer, a dictation module (one-way audio), the Ramble module (voice capture and processing), and a conversation module (bi-directional audio, reserved for future features). Raw PCM audio streams directly to Gemini — no separate transcription step — so language detection, speech recognition, and semantic understanding happen in a single pass. The model autonomously invokes addTask/editTask/deleteTask tools as the user speaks, and session-resumption tokens let mobile users switch apps or drop connectivity without losing state.

## Key decisions
- Stream raw PCM instead of pre-transcribing: one model pass cuts latency and preserves semantic context.
- Proactive tool calling — the model decides when to add/edit/delete tasks without explicit voice commands.
- Simple context injection (user metadata straight into the system prompt) outperformed more complex retrieval strategies.
- Session resumption tokens as a first-class requirement for mobile reliability.
- LLM-as-judge validation: a second Gemini model checks that outputs semantically match speaker intent, monitored per language.

## Stack
Gemini Live API, Gemini Flash, Gemini Enterprise Agent Platform; modular provider-agnostic backend (streaming/dictation/ramble/conversation layers); tool-calling into Todoist task APIs.

## Results
Tested across 15+ language variations with 100+ real-world recordings from native speakers with local accents. In Doist's comparisons, Gemini produced the clearest and most consistent task breakdowns among the platforms evaluated. Ramble became a hallmark feature driving both B2C and B2B adoption, and the launch deepened Doist's partnership with Google to manage high API usage.

## Takeaways
- For voice UX, skipping the transcription hop and letting one multimodal model do recognition + understanding is both faster and more accurate.
- Simple, direct context beats elaborate retrieval when the task is well scoped.
- Non-deterministic voice features need a semantic evaluation harness (real recordings + LLM-as-judge per language) rather than exact-output tests.
