---
id: cs2188
title: Adaptive Interruption Handling for Voice AI Agents
company: LiveKit
primary_category: audio
sub_category: audio-classification
year: 2024
source_url: https://livekit.com/blog/adaptive-interruption-handling
tags: [barge-in, interruption-detection, voice-AI, audio-classifier, backchanneling, voice-agents, real-time]
---

# Adaptive Interruption Handling for Voice AI Agents
**LiveKit** · 2024 · [source](https://livekit.com/blog/adaptive-interruption-handling)

## Problem
Voice agents using plain Voice Activity Detection (VAD) treat any detected speech as a barge-in, so backchannels ("mm-hmm"), coughs, and background noise cut the agent off mid-sentence, making conversations feel jittery and robotic. The agent needs to distinguish genuine interruptions from incidental sounds, fast.

## Approach / System design
LiveKit trained a dedicated audio-based interruption classifier: an audio encoder feeding a CNN that analyzes acoustic characteristics in the first few hundred milliseconds of detected speech to recognize the signatures of true interruptions versus backchannels and noise. Because real agent-interaction logs contain little usable interruption data, the model was trained on natural human-to-human conversations, with data-enrichment pipelines mixing in varied noise for real-world robustness. The model is served centrally from LiveKit Cloud data centers rather than bundled into agent containers.

## Key decisions
- Train on human-human conversational data instead of scarce agent-interaction examples.
- Classify from acoustics only, within the first few hundred milliseconds, to keep decisions fast enough for live conversation.
- Design for multilingual generalization rather than memorizing language-specific patterns.
- Centralized cloud deployment for the classifier instead of per-container bundling.

## Stack
Audio encoder + CNN classifier over waveform acoustic patterns, noise-mixing data enrichment pipeline, deployed in LiveKit Cloud alongside VAD in the voice-agent pipeline.

## Results
86% precision and 100% recall (at 500ms overlap); rejects 51% of VAD false positives; detects true interruptions 64% faster than VAD; inference in 30ms or less; median 216ms of audio needed to trigger.

## Takeaways
Generic VAD can't solve conversational-flow problems — a small specialized model trained on the right data source (real human conversations, noise-enriched) beats heuristics on both false barge-ins and reaction speed.
