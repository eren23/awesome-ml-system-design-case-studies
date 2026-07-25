---
id: cs2296
title: Improving Generative Ad Text on Facebook using Reinforcement Learning
company: Meta
primary_category: rl
sub_category: policy-optimization
year: 2025
source_url: https://arxiv.org/abs/2507.21983
tags: [rlpf, llm, advertising, ad-text-generation, facebook, performance-feedback]
---

# Improving Generative Ad Text on Facebook using Reinforcement Learning
**Meta** · 2025 · [source](https://arxiv.org/abs/2507.21983)

## Problem
LLMs need post-training to be useful for specific production tasks, but the actual economic impact of RL-based post-training had gone largely unmeasured in real deployments. For Facebook's Text Generation feature — which rewrites ad text variations for advertisers — supervised fine-tuning on curated ad examples teaches the model what "good" ads look like, but not which ads actually perform.

## Approach / System design
Meta built AdLlama, a Llama-based model trained with "reinforcement learning with performance feedback" (RLPF): historical ad performance data serves as the reward signal, pushing the model toward generating ad text that drives real engagement rather than merely imitating curated examples. AdLlama was deployed inside Facebook's ad-creation Text Generation feature and evaluated against a supervised imitation baseline trained on curated ads in a large-scale production A/B test.

## Key decisions
- Optimize against measured ad performance (historical metrics) instead of human preference labels or curation alone.
- Keep a supervised imitation model as the comparison baseline to isolate the value added by RL post-training.
- Measure impact in an ecologically valid setting — a live production experiment with real advertisers — rather than offline benchmarks.

## Stack
AdLlama, an LLM (Llama family) post-trained with RLPF using historical ad performance as reward; served inside Facebook's ad Text Generation feature. Further training/serving details are not covered in the source.

## Results
- 6.7% improvement in click-through rate over the supervised baseline (p=0.0296).
- 10-week A/B test spanning nearly 35,000 advertisers and roughly 640,000 generated ad variations.
- Advertisers also generated more ad variations with AdLlama, suggesting higher satisfaction with the outputs.
- Described as the largest study to date of generative AI in an ecologically valid production setting.

## Takeaways
Rewarding an LLM with real downstream performance data (RLPF) turns post-training into measurable business value: a modest-sounding CTR lift at Facebook scale is substantial, and it demonstrates that performance-feedback RL beats imitation of curated examples for outcome-driven generation tasks.
