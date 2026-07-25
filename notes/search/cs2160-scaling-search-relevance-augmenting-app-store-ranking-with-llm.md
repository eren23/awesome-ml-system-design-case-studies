---
id: cs2160
title: "Scaling Search Relevance: Augmenting App Store Ranking with LLM-Generated Judgments"
company: Apple
primary_category: search
sub_category: learning-to-rank
year: 2026
source_url: https://machinelearning.apple.com/research/augmenting-app
tags: [app-store, LLM, relevance-labels, learning-to-rank, knowledge-distillation, A/B-test]
---

# Scaling Search Relevance: Augmenting App Store Ranking with LLM-Generated Judgments
**Apple** · 2026 · [source](https://machinelearning.apple.com/research/augmenting-app)

## Problem
App Store ranking optimizes two complementary objectives — behavioral relevance (clicks, downloads) and textual relevance (semantic query-result match) — but the training data is lopsided: behavioral labels are abundant while expert textual relevance labels are scarce, limiting how well the ranker can learn semantic matching.

## Approach / System design
Apple systematically evaluated LLM configurations for generating textual relevance judgments at scale. A specialized, fine-tuned smaller LLM proved significantly better at label quality than a much larger pre-trained model, so it became the label generator. The team then produced millions of synthetic textual relevance labels and used them to augment the behavioral signals training the production ranker.

## Key decisions
- Keep both objectives in the ranker — behavioral and textual relevance — rather than collapsing to one.
- Choose a fine-tuned small LLM over a large general-purpose one for label generation, based on measured label quality.
- Use LLM judgments to fill the data gap (label augmentation) instead of putting an LLM in the serving path.

## Stack
Fine-tuned LLM as an offline relevance-judgment generator; production learning-to-rank system for App Store search trained on combined behavioral and LLM-generated textual labels. Model and infrastructure specifics are not covered in the source.

## Results
Offline, NDCG improved on both behavioral and textual relevance simultaneously — a Pareto improvement rather than a trade-off. A worldwide A/B test showed a statistically significant +0.24% increase in conversion rate, with the strongest gains on tail queries where behavioral signals are unreliable.

## Takeaways
LLMs earn their keep in search as offline force multipliers for scarce human judgment: millions of synthetic labels moved a production metric without adding serving cost. Fine-tuned specialists beat bigger generalists for judgment tasks, and the payoff concentrates exactly where behavioral data is weakest — the tail.
