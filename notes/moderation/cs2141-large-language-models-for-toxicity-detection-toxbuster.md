---
id: cs2141
title: Large Language Models for Toxicity Detection: ToxBuster
company: Ubisoft
primary_category: moderation
sub_category: toxicity
year: 2025
source_url: https://www.ubisoft.com/en-us/studio/laforge/news/54QiUaTH5oCX7MUhSSgrGy/large-language-models-for-toxicity-detection-toxbuster
tags: [llm, bert, in-game-chat, toxicity, gaming, real-time, production, multi-language]
---

# Large Language Models for Toxicity Detection: ToxBuster
**Ubisoft** · 2025 · [source](https://www.ubisoft.com/en-us/studio/laforge/news/54QiUaTH5oCX7MUhSSgrGy/large-language-models-for-toxicity-detection-toxbuster)

## Problem
In-game chat toxicity harms players, particularly marginalized groups, but is hard to detect automatically: messages are short, colloquial, abbreviation-heavy, and their meaning depends on who is speaking to whom and what happened earlier in the conversation.

## Approach / System design
ToxBuster, built by Ubisoft La Forge, is a BERT-based model that classifies chat lines in context. Each line is analyzed alongside conversation history and game metadata, with speaker segmentation carrying three attributes: PlayerID (who is speaking), ChatType (global/team/private), and TeamID (team affiliation). Output is multi-category toxicity classification rather than a binary toxic/non-toxic flag, running in real time. The team also built a dedicated identity-bias analysis: 16,008 synthetic chat lines generated from 22 sentence templates and 46 identity terms, with a random forest classifier used for ground-truth annotation, to find identity terms the model over- or under-flags relative to humans.

## Key decisions
- Use pre-trained BERT rather than training from scratch, to inherit linguistic nuance.
- Feed chat history plus speaker/team metadata instead of scoring isolated messages.
- Classify into multiple toxicity categories, not just binary.
- Treat bias measurement as a first-class workstream alongside accuracy.

## Stack
BERT core model; random forest for bias-annotation ground truth; training data from real chat in Rainbow Six Siege, For Honor, and DOTA 2, plus the Civil Comments dataset.

## Results
Strong F1 scores across the tested datasets (the article reports figures in charts rather than headline numbers). Per the catalog summary, the deployed system spans multiple game titles with multi-language support and identifies on average about 50 toxic players per game per day. The bias analysis surfaced identity terms with mismatched reactivity versus human annotation.

## Takeaways
- Conversation and game context materially improves toxicity detection over per-message scoring.
- Deployed moderation models need continuous bias auditing, not a one-time fairness check.
- Human-AI collaboration remains necessary to separate friendly banter from genuine toxicity in game-specific language.
