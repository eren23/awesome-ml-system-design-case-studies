---
id: cs1808
title: "LiveKit — Solving End-of-Turn Detection: Turn Detector v1 for Voice Agents"
company: LiveKit
primary_category: audio
sub_category: audio-classification
year: "2025"
source_url: https://livekit.com/blog/solving-end-of-turn-detection
tags: [voice-agents, turn-detection, end-of-turn, prosody, open-source]
---

# LiveKit — Solving End-of-Turn Detection: Turn Detector v1 for Voice Agents
**LiveKit** · 2025 · [source](https://livekit.com/blog/solving-end-of-turn-detection)

## Problem
Voice activity detection alone is a poor signal for end-of-turn in conversational agents because it can not distinguish a natural pause mid-sentence from the speaker genuinely finishing their turn. Triggering an agent response too early interrupts the user; triggering too late creates an unnatural conversation cadence. A better signal must incorporate both what was said and how it was said.

## Approach / System design
Turn Detector v1 fuses two parallel branches: a semantic branch that reads the textual content of the utterance to assess whether the thought is complete, and an acoustic branch that models timing and prosodic features to detect the characteristic falling intonation and pause patterns that mark turn completion. The outputs of both branches are combined to produce a single end-of-turn probability that drives the agent's response trigger.

## Key decisions
Running semantic and acoustic analysis in parallel rather than sequentially keeps latency low while preserving both types of signal. Supporting 14 languages out of the box was a deliberate product decision to make the tool broadly useful without per-language customisation. The model and code were released as open source to allow the voice-agent community to inspect, fine-tune, and integrate it freely.

## Stack
Custom semantic branch, acoustic/prosody branch, multi-branch fusion architecture; open-source release.

## Results
Turn Detector v1 covers 14 languages and replaces VAD-only endpointing in LiveKit voice agent pipelines. Specific latency or accuracy benchmarks are not covered in the source.

## Takeaways
Reliable end-of-turn detection requires combining content-level understanding with acoustic-prosodic signals; either dimension alone produces unacceptable error rates in production voice agents. Open-sourcing domain-specific components like this lowers the barrier to entry for developers building conversational AI products.
