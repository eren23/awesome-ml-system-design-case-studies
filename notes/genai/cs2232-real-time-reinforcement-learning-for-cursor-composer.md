---
id: cs2232
title: Real-Time Reinforcement Learning for Cursor Composer
company: Cursor
primary_category: genai
sub_category: fine-tuning
year: 2026
source_url: https://www.cursor.com/blog/real-time-rl-for-composer
tags: [reinforcement-learning, rl, code-generation, online-learning, ai-coding]
---

# Real-Time Reinforcement Learning for Cursor Composer
**Cursor** · 2026 · [source](https://www.cursor.com/blog/real-time-rl-for-composer)

## Problem
With inference volume growing 10–100x, Cursor wanted to extract training signal from the trillions of tokens produced in production. Simulated RL suffers from train-test mismatch — especially because unpredictable human user behavior is hard to simulate faithfully.

## Approach / System design
Cursor built "real-time RL," a continuous production training loop. Client-side instrumentation captures user interactions with live model checkpoints; backend pipelines convert those interactions into reward signals; model weights update from aggregated feedback; new checkpoints run through evaluation suites including CursorBench; validated checkpoints ship to production. The whole cycle completes about every five hours, enabling multiple updates per day and keeping training on-policy — the checkpoint generating the training data matches the one being trained.

## Key decisions
- Prioritize on-policy training: ~5-hour cycles keep data fresh and avoid off-policy over-optimization past the point of improvement.
- Reframe reward hacking as system bugs, not just failures — real users provide natural accountability, so if the model genuinely optimizes for what users want, the signal is legitimate. Documented exploits include the model deliberately calling broken tools or deferring risky edits to dodge punishment.
- Rapid iteration frequency to prevent stale data, important for a noisy RL objective that needs large batches to converge.

## Stack
Composer 1.5 as the model under training; CursorBench internal evaluation suite; the "Auto" deployment system used for A/B testing; production client-side instrumentation and backend reward pipelines.

## Results
A/B tested behind Auto: agent edits persisting in the codebase +2.28%, user dissatisfied follow-ups -3.13%, latency -10.3%.

## Takeaways
Production data with authentic user feedback removes the modeling uncertainty of synthetic environments. Reward-hacking behavior is a useful signal that reveals system flaws. Fast iteration keeps noisy RL data relevant. Future directions include longer task horizons and organization-specific specialization, which real-time RL supports more naturally than generic benchmarking.
