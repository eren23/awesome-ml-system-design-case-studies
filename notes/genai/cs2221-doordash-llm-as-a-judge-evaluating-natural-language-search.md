---
id: cs2221
title: 'DoorDash LLM-as-a-Judge: Evaluating Natural Language Search'
company: DoorDash
primary_category: genai
sub_category: eval
year: 2025
source_url: https://careersatdoordash.com/blog/doordash-llm-as-a-judge-evaluating-natural-language-search/
tags: [llm-as-judge, natural-language-search, evaluation, search]
---

# DoorDash LLM-as-a-Judge: Evaluating Natural Language Search
**DoorDash** · 2025 · [source](https://careersatdoordash.com/blog/doordash-llm-as-a-judge-evaluating-natural-language-search/)

## Problem
DoorDash's natural language search (NLS) needed to judge whether queries like "cozy date night dinner" returned relevant results. Traditional search metrics (CTR, null rate) fail on novel queries with no history, and human annotation was slow (2–5 day cycles, weeks to train contractors) and unreliable: an audit of 6,824 query-store judgments found 30%+ misalignment on boundary cases like "mostly relevant" — exactly where supervised models learn most.

## Approach / System design
A three-phase workflow. Phase 1 — rubric redesign: replace vague multi-grade scales (0/0.5/0.8/1.0) with binary facet questions ("Does this store serve tacos or equivalent?"), decomposing composite intent into independent, evidence-anchored checks (cuisine, price, speed, location, dietary). Phase 2 — judge calibration: use OpenAI's o3-mini to grade query-store pairs against adjudicated human consensus (not noisy individual labels), iterating on prompts and context enrichment. Phase 3 — automation: deploy the calibrated judge for daily production monitoring and PR-level guardrails that block regressions before shipping. The judge reasons over each facet sequentially (chain-of-thought) to cut variance.

## Key decisions
- Binary over multi-grade scales — each binary question leaves little room for interpretation.
- Independent, non-overlapping facets anchored to observable store data.
- Per-facet metrics instead of a single aggregate NDCG, which exposed that speed and location lagged while cuisine and price were strong.
- Treat the rubric as a versioned, evolving artifact.

## Stack
OpenAI o3-mini as the judge for the audit; a Qwen3-based reranker as the supervised baseline; evaluation ideas referenced from G-EVAL, TaoSR1, LORE, SAGE, and RocketEval.

## Results
Label-noise audit: 19 of 35 manually reviewed cases were incorrect, 30%+ disagreement on boundary judgments. The Qwen3 reranker hit only AUC 0.56 on human labels (barely above random), indicating label quality — not architecture — was the bottleneck. Per-facet NDCG@5: cuisine and price ~0.84, discovery queries ~0.743; ~40% duplicate stores across different consumer queries. No end-to-end production NLS metrics were reported.

## Takeaways
Human labels aren't ground truth — noise concentrates at decision boundaries and destabilizes supervised training; LLM disagreement is a lens on rubric flaws, not annotator incompetence. Decomposition into binary independent facets reduces variance, missing item-level context (not judge limitations) caused many failures, and evaluation must evolve with the product. Practical path: start with binary scales, measure per-facet from day one, automate early, and version rubrics.
