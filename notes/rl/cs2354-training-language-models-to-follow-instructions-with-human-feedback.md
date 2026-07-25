---
id: cs2354
title: Training language models to follow instructions with human feedback (InstructGPT)
company: OpenAI
primary_category: rl
sub_category: rlhf
year: 2022
source_url: https://arxiv.org/abs/2203.02155
tags: [rlhf, ppo, reward-model, instruction-following, alignment, llm, human-feedback]
---

# Training language models to follow instructions with human feedback (InstructGPT)
**OpenAI** · 2022 · [source](https://arxiv.org/abs/2203.02155)

## Problem
Making language models bigger does not make them better at following user intent: large LMs still produce untruthful, toxic, or simply unhelpful outputs. OpenAI needed a way to align GPT-3's behavior with what users actually want across a broad distribution of real prompts.

## Approach / System design
A three-step pipeline built on real usage. First, supervised fine-tuning: labelers write demonstrations of desired behavior for prompts (labeler-written and submitted through the OpenAI API), and GPT-3 is fine-tuned on them. Second, reward modeling: labelers rank multiple model outputs per prompt, and a reward model is trained on these comparisons. Third, reinforcement learning: the SFT model is further optimized with PPO against the reward model. The resulting models are called InstructGPT.

## Key decisions
- Train on the real API prompt distribution rather than academic benchmarks, so alignment targets actual usage.
- Use human preference rankings (not just demonstrations) as the optimization signal, letting the reward model capture graded judgments.
- Optimize with RL against the learned reward model rather than stopping at supervised fine-tuning.
- Track the "alignment tax" on public NLP benchmarks and mitigate regressions.

## Stack
Not covered in the source beyond the GPT-3 model family and the RLHF pipeline (SFT, reward model, PPO).

## Results
Outputs from the 1.3B-parameter InstructGPT were preferred by humans over outputs from the 175B GPT-3 — a 100x parameter advantage overcome by alignment. InstructGPT also improved truthfulness and reduced toxic output generation, with minimal performance regressions on public NLP datasets.

## Takeaways
Alignment is a far more efficient axis of improvement than scale: a small aligned model beat a 100x larger unaligned one on human preference. The demonstrated SFT → reward model → PPO recipe became the canonical production RLHF pipeline and the direct precursor to ChatGPT.
