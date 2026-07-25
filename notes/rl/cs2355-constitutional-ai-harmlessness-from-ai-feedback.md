---
id: cs2355
title: "Constitutional AI: Harmlessness from AI Feedback"
company: Anthropic
primary_category: rl
sub_category: rlhf
year: 2022
source_url: https://arxiv.org/abs/2212.08073
tags: [rlaif, constitutional-ai, rlhf, alignment, llm, self-critique, harmlessness]
---

# Constitutional AI: Harmlessness from AI Feedback
**Anthropic** · 2022 · [source](https://arxiv.org/abs/2212.08073)

## Problem
Training language models to be harmless traditionally requires large volumes of human labels identifying harmful outputs — expensive, slow, and hard to scale as models improve. Anthropic wanted to reduce the human-oversight burden for harmlessness while keeping models helpful and non-evasive, using only a small set of written principles as human input.

## Approach / System design
The method replaces human harmlessness labels with a "constitution" — a written set of principles — and a two-phase training pipeline. In the supervised phase, the model generates responses to harmful prompts, critiques its own outputs against constitutional principles, revises them, and is then fine-tuned on the revised responses. In the RL phase ("RL from AI Feedback", RLAIF), the fine-tuned model generates response pairs, an AI evaluator judges which response better satisfies the constitution, a preference model is trained on this AI-labeled comparison data, and that preference model serves as the reward signal for RL training.

## Key decisions
- Encode harmlessness as explicit written principles rather than as thousands of implicit human judgments.
- Use the model itself for critique-and-revision, bootstrapping better training data from its own outputs.
- Replace human preference labels with AI-generated preference labels for the harmlessness reward signal.
- Use chain-of-thought reasoning during critique/evaluation, improving both performance and transparency.
- Train the assistant to engage with harmful queries by explaining its objections instead of refusing evasively.

## Stack
Not covered in the source beyond the model/training pipeline itself.

## Results
The approach produced a helpful, harmless assistant that is non-evasive on sensitive queries, demonstrating that harmlessness training can scale with dramatically fewer human annotations. Detailed benchmark numbers are not covered in the fetched source content.

## Takeaways
AI feedback can substitute for human feedback on the harmlessness axis when anchored to explicit principles, making safety training scale with model capability rather than annotation budget. Encoding values as an inspectable constitution also makes the alignment target auditable, and self-critique with chain-of-thought turns the model into a useful generator of its own training signal.
