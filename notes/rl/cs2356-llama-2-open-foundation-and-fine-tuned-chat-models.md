---
id: cs2356
title: "Llama 2: Open Foundation and Fine-Tuned Chat Models"
company: Meta
primary_category: rl
sub_category: rlhf
year: 2023
source_url: https://arxiv.org/abs/2307.09288
tags: [rlhf, ppo, rejection-sampling, reward-model, alignment, llm, open-source, chat]
---

# Llama 2: Open Foundation and Fine-Tuned Chat Models
**Meta** · 2023 · [source](https://arxiv.org/abs/2307.09288)

## Problem
Meta wanted openly released chat models (7B–70B parameters) competitive with proprietary assistants, which required building a full production-grade alignment pipeline — SFT, reward modeling, and iterative RLHF — that balances helpfulness with safety at scale.

## Approach / System design
Llama 2-Chat is produced by a staged pipeline on top of the pretrained Llama 2 base models. SFT uses a deliberately small set of high-quality vendor annotations (~27,540 examples) after finding quality beats quantity. Two separate reward models are trained — one for helpfulness, one for safety — initialized from pretrained checkpoints, trained with a binary ranking loss augmented by preference-rating margins, on 1.4M+ internal comparisons plus open-source preference data. RLHF then proceeds iteratively: rejection sampling first (sample K outputs from the 70B model, keep the reward-model-best, fine-tune on them; smaller models distill from the 70B's selections), followed by PPO with a combined helpfulness/safety reward and a KL penalty against the base policy. Ghost Attention (GAtt) keeps multi-turn system instructions in force by synthetically prepending them during training and zeroing loss on prior turns. Safety work adds supervised safety fine-tuning on adversarial prompts (illicit activities, hateful content, unqualified advice), safety context distillation (train with safety preprompts, remove them at inference), and adversarial prompts in safety RLHF.

## Key decisions
- Small, high-quality SFT set over large third-party corpora.
- Two specialized reward models instead of one, acknowledging the helpfulness/safety tension.
- Margin-augmented ranking loss for reward models, improving accuracy on clearly separable pairs.
- Rejection sampling before PPO — broad exploration (K samples per prompt) before fine-grained policy optimization.
- GAtt as a data-side fix for multi-turn instruction drift.
- Distill safety behavior into weights via context distillation rather than relying on inference-time preprompts.

## Stack
Not covered in the source beyond the training pipeline (reward models initialized from Llama 2 checkpoints; RLHF via rejection sampling and PPO).

## Results
Meta's reward models outperformed all baselines including GPT-4 on their evaluation, with the helpfulness model at 70.6% and the safety model at 64.3% accuracy on internal test sets. In human evaluation on ~4,000 prompts, Llama 2-Chat 70B achieved a 36% win rate and 31.5% tie rate against ChatGPT, and the 34B model won more than 75% of comparisons against similarly sized Vicuna-33B and Falcon-40B. GAtt held system-message adherence over 20+ turns. Safety RLHF added long-tail robustness without hurting helpfulness.

## Takeaways
Iterated RLHF — successive reward-model generations, rejection sampling, then PPO — compounds: each round of better data and better reward models lifts the policy. Splitting helpfulness and safety into separate reward models makes the trade-off explicit and tunable, and annotation quality matters more than volume at the SFT stage. The paper made a previously proprietary-grade alignment recipe public.
