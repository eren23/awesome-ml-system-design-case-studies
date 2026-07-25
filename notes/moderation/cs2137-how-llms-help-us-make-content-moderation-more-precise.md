---
id: cs2137
title: How LLMs Help Us Make Content Moderation More Precise
company: Grab
primary_category: moderation
sub_category: policy-enforcement
year: 2025
source_url: https://www.grab.com/inside-grab/stories/how-large-language-models-help-us-make-more-precise-content-moderation-decisions/
tags: [llm, fine-tuning, two-tier, content-moderation, user-generated-content, production]
---

# How LLMs Help Us Make Content Moderation More Precise
**Grab** · 2025 · [source](https://www.grab.com/inside-grab/stories/how-large-language-models-help-us-make-more-precise-content-moderation-decisions/)

## Problem
Grab must screen huge volumes of user-generated content — merchant catalogues and user reviews — for policy violations. Simple automated filters alone lack the context to make nuanced calls (e.g., telling tobacco apart from e-cigarettes), while routing everything ambiguous to human moderators is slow and expensive.

## Approach / System design
A two-tier pipeline:
- **Tier 1 — automated screening:** small, specialised models (keyword filters, image-screening models) rapidly scan all content and flag under 5% as potential violations.
- **Tier 2 — LLM assessment:** an LLM makes context-aware decisions on the flagged subset, driven by policy definitions expressed as prompts. Medium-confidence cases escalate to human moderators, keeping people in the loop only where needed.

## Key decisions
- Started introducing LLMs into Tier 2 in 2023, expanding coverage through Q3 2024.
- Encoded policies as prompts rather than per-policy models, giving flexibility across violation types.
- Retained human review for ambiguous, medium-confidence cases instead of full automation.

## Stack
Small specialised classifiers (keyword and image screening) in Tier 1; LLMs with policy prompts in Tier 2; human moderation queue as the final tier. Ongoing fine-tuning on internal data. Specific model names are not covered in the source.

## Results
- 90% reduction in human moderation effort.
- Moderation SLA cut from days to minutes.
- Tier 1 keeps the flagged volume under 5% of total content.

## Takeaways
- Cheap filters in front of LLMs make LLM-grade judgment affordable at platform scale.
- Prompt-encoded policy is faster to update than retraining per-policy classifiers.
- Remaining gaps: latency on image inputs and LLM knowledge of local languages and domain-specific topics, being addressed via fine-tuning on internal data.
