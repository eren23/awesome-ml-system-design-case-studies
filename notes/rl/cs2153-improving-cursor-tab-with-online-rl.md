---
id: cs2153
title: Improving Cursor Tab with Online RL
company: Cursor
primary_category: rl
sub_category: policy-optimization
year: 2025
source_url: https://cursor.com/blog/tab-rl
tags: [online-rl, code-completion, real-time-training, policy-deployment, developer-tools]
---

# Improving Cursor Tab with Online RL
**Cursor** · 2025 · [source](https://cursor.com/blog/tab-rl)

## Problem
Cursor Tab predicts a developer's next action across the codebase, but too many suggestions were noise: false positives that get rejected break coding flow. The hard part is not only suggesting well but knowing when to stay silent, since even a perfect model cannot always know user intent.

## Approach / System design
Instead of bolting on a post-hoc filter (the GitHub Copilot contextual-filter approach), Cursor changes the Tab model itself with policy gradient RL so it learns to avoid emitting low-quality suggestions. Rewards encourage suggestions that get accepted and penalize showing suggestions with low acceptance probability. The loop is genuinely online: updated models ship to users continuously, their acceptance feedback becomes fresh on-policy training data, and the cycle repeats several times a day.

## Key decisions
- Modify the policy directly via policy gradients rather than training a separate acceptance-prediction filter.
- Ship checkpoints every 1.5-2 hours so collected data stays on-policy — a requirement of the Policy Gradient Theorem the training relies on.
- Shape rewards to jointly optimize acceptance rate and suggestion restraint (when not to suggest).

## Stack
Policy gradient optimization (Policy Gradient Theorem), PyTorch, stochastic gradient descent, trained on live user feedback from 400M+ daily Tab requests, with a rapid deployment pipeline for multiple rollouts per day.

## Results
The RL-trained Tab model makes 21% fewer suggestions while achieving a 28% higher accept rate on the suggestions it does show.

## Takeaways
Online RL turns a product's own usage stream into a continuously improving training signal, outpacing periodic offline releases. The operational price is real — infrastructure to deploy models every couple of hours — because on-policy data is what makes the math valid; and optimizing "when to shut up" can matter as much as raw suggestion quality.
