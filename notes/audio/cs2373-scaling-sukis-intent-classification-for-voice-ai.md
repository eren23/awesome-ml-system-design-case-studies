---
id: cs2373
title: Scaling Suki's Intent Classification for Voice AI
company: Suki
primary_category: audio
sub_category: asr
year: 2024
source_url: https://www.suki.ai/blog/scaling-sukis-command-understanding-building-fast-and-accurate-intent-classification-for-clinical-voice-assistants/
tags: [intent-classification, NLU, clinical-voice, voice-commands, voice-assistant, healthcare]
---

# Scaling Suki's Intent Classification for Voice AI
**Suki** · 2024 · [source](https://www.suki.ai/blog/scaling-sukis-command-understanding-building-fast-and-accurate-intent-classification-for-clinical-voice-assistants/)

## Problem
Suki's clinical voice assistant had to interpret natural, highly variable clinician commands at scale while keeping responses under 300ms — fast enough that LLM API calls were off the table. Additional constraints: limited proprietary medical training data, and the need to add new command types quickly without large labeling efforts.

## Approach / System design
A dual-component NLU architecture:
- **Intent classification** as retrieval rather than a fixed classifier: sentence encoders finetuned with contrastive learning, with k-nearest-neighbor voting over vector similarity, giving few-shot capability for new intents.
- **Slot filling** with a Flan-T5 model fine-tuned via LoRA for extractive tasks, accelerated by custom n-gram caching that uses a lightweight part-of-speech tagger to speed up medical term retrieval.
Limited training data was expanded with LLM-generated synthetic examples while preserving clinical accuracy.

## Key decisions
- Contrastive finetuning with semi-hard triplet loss to separate similar-but-different commands (e.g., "go to his HPI file" vs. "move his HPI file here").
- Retrieval + kNN voting instead of a traditional softmax classifier, so new intents work few-shot without retraining.
- Purpose-built small models over LLM API calls to satisfy the latency budget.
- n-gram caching keyed off POS tagging to cut inference latency on medical terms.

## Stack
Sentence encoders with contrastive finetuning; Flan-T5 with LoRA; vector store for semantic search; lightweight POS tagger; LLM-based synthetic data generation.

## Results
- 98% accuracy on real-world clinical voice commands.
- Sub-300ms response times in production.
- 62% latency reduction versus standard HuggingFace inference; 133% faster than a GPT-4 baseline.
- 90%+ accuracy on new intents with only 15 training samples.

## Takeaways
For latency-bound production NLU, purpose-built compact models with domain-specific optimization beat generic LLM calls. Contrastive learning plus synthetic data augmentation delivers high accuracy despite scarce domain data, and framing classification as retrieval makes the system extensible — new commands ship with a handful of examples instead of a retraining cycle.
