---
id: cs2102
title: How to Build Smarter Turn Detection for Voice AI
company: Speechmatics
primary_category: audio
sub_category: audio-classification
year: 2024
source_url: https://blog.speechmatics.com/semantic-turn-detection
tags: [turn-detection, small-language-model, SLM, voice-agents, end-of-turn]
---

# How to Build Smarter Turn Detection for Voice AI
**Speechmatics** · 2024 · [source](https://blog.speechmatics.com/semantic-turn-detection)

## Problem
Voice agents that rely on silence-based Voice Activity Detection (VAD) for end-of-turn detection interrupt users constantly: VAD only understands audio patterns, so it can't tell whether a pause means the user is thinking, checking information, or actually done. The result is premature interruptions, wasted LLM calls on incomplete utterances, and a frustrating experience.

## Approach / System design
Speechmatics adds semantic turn detection using an instruction-tuned Small Language Model. The running transcript is formatted as a ChatML conversation, and instead of generating text, the system reads the model's log-probability that the next token is the end-of-turn marker (`<|im_end|>`). A high probability means the utterance is semantically complete and the agent may respond; a low one means keep listening even through silence. The reference implementation uses SmolLM2-360M-Instruct (360M parameters), keeps at most the 4 most recent messages of history to stay within latency budgets, applies a default probability threshold of 0.03 (tunable per deployment), and runs on CPU. Semantic detection is meant to combine with, not replace, acoustic VAD.

## Key decisions
- Reuse an off-the-shelf instruct SLM's chat-format training rather than training a dedicated turn-detection model — the `<|im_end|>` token already encodes "turn is complete."
- Score a single next-token probability instead of generating, making inference cheap and fast enough for real time on CPU.
- Truncate context to 4 messages and expose the threshold as a tunable knob per deployment.
- Pair semantic signal with VAD: semantics for precision, acoustics for recall.

## Stack
Python, PyTorch, Hugging Face Transformers/AutoTokenizer; HuggingFaceTB/SmolLM2-360M-Instruct; ChatML conversation formatting; CPU inference.

## Results
No empirical benchmark numbers are published. Claimed benefits are qualitative: fewer premature interruptions, lower API cost from avoiding LLM calls on false end-of-turn triggers, and better conversational UX.

## Takeaways
- End-of-turn probability read from an instruct model's next-token distribution is an elegant, nearly-free semantic turn signal.
- Sub-billion-parameter SLMs are sufficient for this task and deployable on CPU within real-time budgets.
- Text-based semantics still miss tone and cadence; the authors point to audio-native models as the eventual full solution.
