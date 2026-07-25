---
id: cs2303
title: "RELATE: A Reinforcement Learning-Enhanced LLM Framework for Advertising Text Generation"
company: Baidu
primary_category: rl
sub_category: policy-optimization
year: 2026
source_url: https://arxiv.org/abs/2602.11780
tags: [rl-for-nlg, advertising, llm, text-generation, ctcvr, policy-optimization, compliance]
---

# RELATE: A Reinforcement Learning-Enhanced LLM Framework for Advertising Text Generation
**Baidu** · 2026 · [source](https://arxiv.org/abs/2602.11780)

## Problem
Industrial ad-creative systems typically work in two disconnected stages: generate candidate ad texts, then separately select/optimize them for performance metrics like CTR. The split creates misaligned objectives and an inefficient funnel — the generator doesn't know what the optimizer wants, so the pipeline can't reach globally optimal ad text, and compliance is enforced after the fact.

## Approach / System design
RELATE replaces the two-stage paradigm with a single end-to-end framework: ad text generation is treated as a policy-learning problem where an LLM generator is trained with reinforcement learning against rewards that encode both performance and compliance. Performance and policy-constraint objectives are modeled as multi-dimensional rewards, integrating conversion-oriented metrics (beyond click-level signals) directly into the generation process.

## Key decisions
- Unify generation and performance optimization in one model rather than a generate-then-rank funnel.
- Optimize for conversion-oriented CTCVR rather than clicks alone.
- Encode compliance as a reward dimension so policy constraints shape generation instead of filtering it afterward.
- Validate via deployment on Baidu's production advertising platform.

## Stack
LLM-based text generation fine-tuned with reinforcement learning / policy optimization over multi-objective rewards balancing conversion performance and compliance constraints. Specific models and infrastructure are not covered in the source.

## Results
Online deployment on the production advertising platform yielded statistically significant CTCVR improvements while operating under strict policy constraints.

## Takeaways
For ad creative, end-to-end RL-trained generation beats the decoupled generate-then-optimize pattern: putting business and compliance objectives into the reward lets a single policy resolve the trade-offs that a staged funnel structurally cannot.
