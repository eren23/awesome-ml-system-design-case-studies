---
id: cs2409
title: "AGPO: Asymmetric Group Policy Optimization for Verifiable Reasoning and Search Ads Relevance at JD"
company: JD.com
primary_category: ads
sub_category: targeting
year: 2026
source_url: https://arxiv.org/abs/2605.05826
tags: [relevance-scoring, search-ads, LLM, policy-optimization, e-commerce, reasoning]
---

# AGPO: Asymmetric Group Policy Optimization for Verifiable Reasoning and Search Ads Relevance at JD
**JD.com** · 2026 · [source](https://arxiv.org/abs/2605.05826)

## Problem
In search advertising, a mismatch between user queries and served ads degrades user experience and wastes advertiser spend. JD.com needed a semantic relevance gatekeeper capable of filtering out clearly mismatched ads before they enter the ranking stage, a task that requires nuanced reasoning about product and query intent rather than simple keyword overlap.

## Approach / System design
JD.com trains Rele-Ads-8B, a decoder-only large language model, using Asymmetric Group Policy Optimization (AGPO). AGPO is a reinforcement-learning-from-feedback method designed to provide verifiable reward signals for relevance classification tasks. The model acts as a pre-ranking filter, evaluating query–ad pairs and discarding those that fall below a semantic relevance threshold before the main ranking pipeline sees them.

## Key decisions
AGPO introduces asymmetry into the group policy optimization objective to better handle the imbalanced nature of relevance labels in search ads, where irrelevant pairs are far more common than clearly relevant ones. Using a decoder-only architecture rather than a cross-encoder allows the model to benefit from the reasoning capabilities of large pretrained language models while remaining deployable in a production pipeline.

## Stack
The system is built around Rele-Ads-8B, an 8-billion-parameter decoder-only transformer trained with the AGPO policy optimization algorithm. The broader JD Ads Search infrastructure serves as the deployment environment.

## Results
Not covered in the source.

## Takeaways
Framing ad relevance filtering as a verifiable reasoning task and applying asymmetric policy optimization allows a large language model to act as an effective semantic gatekeeper, catching mismatched ads that lexical or embedding-based methods would miss. Inserting such a model at the pre-ranking stage cleanly separates relevance concerns from ranking concerns, improving overall ad quality without overhauling the downstream ranker.
