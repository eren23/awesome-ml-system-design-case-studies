---
id: cs2237
title: Evaluating Netflix Show Synopses with LLM-as-a-Judge
company: Netflix
primary_category: genai
sub_category: eval
year: 2026
source_url: https://netflixtechblog.com/evaluating-netflix-show-synopses-with-llm-as-a-judge-6269251e6f28
tags: [llm-as-judge, content-quality, evaluation, synopsis-generation, llm]
---

# Evaluating Netflix Show Synopses with LLM-as-a-Judge
**Netflix** · 2026 · [source](https://netflixtechblog.com/evaluating-netflix-show-synopses-with-llm-as-a-judge-6269251e6f28)

## Problem
Netflix maintains hundreds of thousands of show synopses with multiple variants per title. Weak synopses frustrate members and contribute to title abandonment, but manually validating quality at that scale is infeasible. Netflix needed automated, consistent quality assessment that still honors editorial standards.

## Approach / System design
Netflix built an LLM-as-a-judge framework with specialized judges for four quality dimensions — precision, clarity, tone, and factuality — evaluating each criterion independently rather than in a single combined prompt. Judges use chain-of-thought reasoning internally but emit concise rationale summaries for creative reviewers. Factuality is handled by an agent-based system where narrow specialized agents check plot, metadata, talent, and awards independently, each with tailored context. Golden datasets for calibration were built with model-in-the-loop consensus alongside human experts.

## Key decisions
- Binary pass/fail scoring instead of Likert scales, which improved agreement among human evaluators.
- Tiered rationales: extended internal reasoning, short surfaced summaries — preserving accuracy without drowning reviewers.
- Consensus scoring via multiple inferences per synopsis with aggregated scores, especially valuable where longer rationales increased score variance.
- Decomposing factuality into narrow specialized agents rather than one monolithic factuality judge.
- Automatic Prompt Optimization (APO) for initial judge tuning.

## Stack
LLM judges with chain-of-thought prompting; Automatic Prompt Optimization; an agent-based factuality-checking system; model-in-the-loop consensus for golden dataset creation.

## Results
The system reached 85%+ agreement with creative writers, with per-criterion accuracies ranging from the mid-80s to low-90s percent. Judge scores showed statistically significant correlation with member behavior metrics (take fraction and abandonment rates), with precision and clarity the most predictive dimensions.

## Takeaways
Specialized judges outperform monolithic ones, and human-AI collaboration during calibration is what makes the judges trustworthy. Spending inference-time compute (longer reasoning, consensus) improves performance with diminishing returns. Validating judges against both expert opinion and real behavioral metrics strengthens credibility.
