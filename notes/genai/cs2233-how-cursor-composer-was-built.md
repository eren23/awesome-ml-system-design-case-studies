---
id: cs2233
title: How Cursor Composer Was Built
company: Cursor
primary_category: genai
sub_category: agents
year: 2025
source_url: https://www.cursor.com/blog/composer
tags: [code-generation, composer, model-training, ai-coding, fine-tuning]
---

# How Cursor Composer Was Built
**Cursor** · 2025 · [source](https://www.cursor.com/blog/composer)

## Problem
Developers want a coding agent that is both frontier-level capable and interactively fast. High-performance models are too slow to keep a developer in flow, while faster models sacrifice intelligence.

## Approach / System design
Composer is a mixture-of-experts language model trained with reinforcement learning on real-world software engineering tasks. During training the model receives a problem description and learns to produce the best response — code edits, plans, or explanations — using the same production tools available in the IDE: file editing, semantic search, terminal commands, and codebase-wide querying. The RL objective explicitly rewards efficient tool use and maximizing parallelism, so the resulting model stays fast enough for interactive use.

## Key decisions
- Speed-aware RL: incentivize efficient tool choices and parallelism, not just correctness.
- Production-aligned evaluation via a custom "Cursor Bench" that measures usefulness to developers, including adherence to a codebase's existing abstractions and engineering practices.
- Infrastructure-first training: low-precision native training with custom MXFP8 MoE kernels rather than post-hoc quantization.

## Stack
Mixture-of-experts architecture; PyTorch and Ray for training; custom MXFP8 MoE kernels across thousands of NVIDIA GPUs; a custom VM scheduler for sandboxed environments; Cursor Bench for evaluation.

## Results
Composer reaches frontier coding quality at roughly 4x the generation speed of similar-capability models. It outperforms "Fast Frontier" models but ranks below GPT-5 and Sonnet 4.5 in absolute capability.

## Takeaways
Speed is a first-class property for agent usability, not an afterthought. RL on authentic workflows produced emergent behaviors like writing tests and fixing linter errors, and heavy infrastructure investment (low-precision MoE training at scale) is what made the approach viable.
