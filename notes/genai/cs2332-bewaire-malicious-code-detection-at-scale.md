---
id: cs2332
title: BewAIre: Malicious Code Detection at Scale
company: Datadog
primary_category: genai
sub_category: agents
year: 2026
source_url: https://www.datadoghq.com/blog/engineering/scaling-malicious-code-detection/
tags: [security, code-analysis, llm, static-analysis, malware-detection, agentic-ai]
---

# BewAIre: Malicious Code Detection at Scale
**Datadog** · 2026 · [source](https://www.datadoghq.com/blog/engineering/scaling-malicious-code-detection/)

## Problem
Attackers increasingly compromise widely used open-source dependencies to distribute malicious code through the software supply chain. Datadog's initial LLM-based pull-request scanning needed to expand to whole dependency packages and upstream registries (npm, PyPI) — without sacrificing accuracy, latency, or blowing up inference costs across tens of thousands of packages.

## Approach / System design
BewAIre is a two-stage agentic LLM pipeline:
- **Filter stage**: a fast, inexpensive screen using previous-generation or cost-optimized models with straightforward prompts; most packages exit here.
- **Review stage**: an agentic investigation by a stronger reasoning model with tool access — GitHub APIs (commit history, contributor details, PR metadata), file-content inspection, dependency-metadata validation, vulnerability database cross-referencing (osv.dev, SCA tools), and static typosquatting checks against domain lists.
- **Large-package handling**: three context strategies were tested — forwarding only the flagged chunk (poor), rechunking the whole package (efficient but error-prone), and the selected approach: a lightweight codemap structural overview plus an on-demand ReadFile tool so the agent inspects only the files it needs. This gave the best accuracy at lower latency and token cost.
- **Upstream monitoring**: a pipeline crawls npm's CouchDB and PyPI RSS feeds every 10 minutes, resolves previous package versions semver-first for diffing, caches artifacts in S3 to avoid redundant downloads, and queues verdicts for manual triage by the Security Research team, which continuously improves a curated dataset of confirmed malicious and benign packages.

## Key decisions
- Stage the pipeline so ~95% of packages never reach the expensive review stage, making costs predictable at scale.
- Give the review agent targeted tools (codemap + ReadFile) instead of stuffing full package contents or naive chunks into context.
- Supplement LLM reasoning with deterministic static checks (typosquatting lists) where rules are cheaper and more reliable.
- Invest in dataset quality via security-partnership-sourced real malware and continuous manual triage feedback.
- Persist crawl state (sequence numbers/timestamps) and cache artifacts for continuous, resumable registry monitoring.

## Stack
Mixed LLM tiers (cost-optimized filter models; state-of-the-art reasoning model for review), agent tooling over GitHub/npm/PyPI APIs and osv.dev, S3 artifact caching, static analysis and SCA integration, manual triage workflow feeding a curated evaluation dataset.

## Results
- PR-analysis accuracy improved from 97.4% to 99.86%; false positives dropped from 17 to 0.
- 95.5% detection rate on malicious packages; 95.2% end-to-end accuracy with the codemap strategy on package scanning.
- Real incident response: detection within 5 minutes of publication and customer notification within 50 minutes.
- Cost per package: about $0.025 at p50 (~5K tokens) and $0.072 at p90 (~87K tokens).

## Takeaways
- Stacked evaluation with early exits is the pattern that makes LLM security scanning affordable at registry scale.
- Agentic tool use (structural overview + selective file reads) beats both full-context and chunking for large-codebase analysis.
- Deterministic preprocessing and LLM reasoning are complements, not competitors.
- Continuous upstream monitoring turns detection into a minutes-scale race that a well-gated pipeline can win.
- Curated, real-world malicious datasets are the foundation the whole system's accuracy rests on.
