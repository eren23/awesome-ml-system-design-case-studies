---
id: cs0816
title: "Listening, Learning, and Helping at Scale: How Machine Learning Transforms Airbnb's Voice Support Experience"
company: Airbnb
primary_category: audio
sub_category: asr
year: 2025
source_url: https://medium.com/airbnb-engineering/listening-learning-and-helping-at-scale-how-machine-learning-transforms-airbnbs-voice-support-b71f912d4760
tags: [voice interface, generative AI, LLM, customer support, genai, nlp, travel, customer-support]
---

# Listening, Learning, and Helping at Scale: How Machine Learning Transforms Airbnb's Voice Support Experience
**Airbnb** · 2025 · [source](https://medium.com/airbnb-engineering/listening-learning-and-helping-at-scale-how-machine-learning-transforms-airbnbs-voice-support-b71f912d4760)

## Problem
Traditional menu-driven IVR forces callers through rigid preset options. Airbnb wanted callers to describe their issue in natural language and be understood and routed correctly — over noisy phone audio and with Airbnb-specific terminology.

## Approach / System design
A conversational IVR pipeline: the caller describes the issue, the audio is transcribed by ASR, intent is classified, and the call is routed either to self-service resources or a human agent. Before handing off, the system gives a clear summary of the understood issue and delivers relevant help articles via SMS/app notification. Help-article retrieval is a two-stage system: semantic (embedding) search followed by LLM-based re-ranking. Paraphrased summaries shown to users are curated by UX writers and matched via text-embedding similarity rather than free-form generation.

## Key decisions
- Domain-adapt ASR for noisy phone audio and Airbnb vocabulary (phrase-list optimization) instead of using a generic model.
- Run intent detection across models in parallel to keep latency imperceptible.
- Hybrid retrieval: semantic search plus LLM ranking, not a single retriever.
- Use curated/standardized paraphrases matched by nearest-neighbor lookup rather than purely generative summaries, for control and consistency.

## Stack
Domain-adapted ASR; multi-model intent classifier; vector database of help-article embeddings; LLM re-ranker; text-embedding similarity for paraphrase matching.

## Results
- Word Error Rate reduced from ~33% to ~10% via domain adaptation.
- Intent-detection latency under ~50ms; article retrieval typically within ~60ms.
- Paraphrase precision above 90% by manual evaluation.
- Higher self-resolution rates and reduced agent dependency among tested users.

## Takeaways
Domain adaptation of ASR is the highest-leverage step for phone support quality. Pairing semantic retrieval with LLM re-ranking, and constraining user-facing text to curated paraphrases, keeps the experience fast and controllable while still feeling conversational.
