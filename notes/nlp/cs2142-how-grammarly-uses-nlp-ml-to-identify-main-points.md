---
id: cs2142
title: How Grammarly Uses NLP & ML to Identify Main Points
company: Grammarly
primary_category: nlp
sub_category: information-extraction
year: 2024
source_url: https://www.grammarly.com/blog/engineering/nlp-ml-identify-main-points/
tags: [extractive-summarization, key-point-identification, lexrank, textrank, bertsum, low-latency, writing-assistance, production]
---

# How Grammarly Uses NLP & ML to Identify Main Points
**Grammarly** · 2024 · [source](https://www.grammarly.com/blog/engineering/nlp-ml-identify-main-points/)

## Problem
Important ideas in emails often get buried in surrounding text or confusing paragraph structure. Grammarly wanted to surface a document's main points to help writers communicate clearly — for 30 million daily active users, at interactive latency.

## Approach / System design
Two-part system: extract main points from the text, and detect where reader attention lands. The team worked with analytical linguists to pin down what counts as a "main point" (distinct from action items like "please fill out the checklist") and used importance scoring to absorb annotator subjectivity. The first production model combined heuristic and semantic features (including LexRank scores) under a reinforcement-learning setup, chosen because labeled data was scarce. Once robust datasets existed, they migrated to a BERTSUM-inspired deep learning model. Selecting the best subset of sentences is combinatorial (10 sentences = 1,024 subsets; 20 = over a million), so they used sampling with weight tracking to escape local minima, pruned obvious non-main-points (salutations, signatures), and cached computations across iterations.

## Key decisions
- Invested in problem definition with linguists before modeling; separated main points from action items.
- Started with heuristics + RL under data scarcity, then swapped in deep learning when data allowed.
- Attacked latency algorithmically (sampling, pruning, caching) rather than only via model changes.

## Stack
LexRank (PageRank-style) as a baseline feature, domain-specific semantic features for email structure, reinforcement-learning scorer, later a BERTSUM-style deep model.

## Results
- Quality: initial model 80% precision / 40% recall; optimized deep model 80% precision / 62% recall.
- Latency: from 1–1.5 s initially to ~8 ms average; ~1 ms for short emails (<10 sentences); ~4 ms at p99.
- Serves 30M daily active users.

## Takeaways
- A crisp, linguist-vetted problem definition made the modeling tractable.
- Hybrid heuristic + learned approaches are a sound bridge while training data accumulates.
- At consumer scale, algorithmic latency work (pruning, caching, sampling) mattered as much as model quality.
