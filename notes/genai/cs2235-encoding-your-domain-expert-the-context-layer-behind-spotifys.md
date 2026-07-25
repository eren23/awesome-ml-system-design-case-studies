---
id: cs2235
title: "Encoding Your Domain Expert: The Context Layer Behind Spotify's Data Assistant"
company: Spotify
primary_category: genai
sub_category: copilots
year: 2026
source_url: https://engineering.atspotify.com/2026/6/encoding-your-domain-expert-the-context-layer-behind-spotifys-data-assistant
tags: [data-assistant, context-layer, rag, domain-knowledge, text-to-sql]
---

# Encoding Your Domain Expert: The Context Layer Behind Spotify's Data Assistant
**Spotify** · 2026 · [source](https://engineering.atspotify.com/2026/6/encoding-your-domain-expert-the-context-layer-behind-spotifys-data-assistant)

## Problem
Spotify processes 1.4 trillion data points daily across more than 70,000 datasets. Data questions flowed to expert knowledge workers through ad-hoc Slack messages — a human bottleneck that could not scale with the organization. An LLM assistant naively fed raw schemas would not know which tables, joins, or definitions are actually correct.

## Approach / System design
Instead of dumping entire schemas into the model, Spotify built a curated context layer of "clusters": domain-specific knowledge bundles owned by data experts. Each cluster has three components — Datasets (schema plus profiling data: cardinality, sample values, partitioning), Pairs (vetted question-SQL examples approved by domain experts), and Docs (business context, terminology, and domain gotchas). The assistant, Vedder, runs a ReAct reasoning loop: select the right cluster context, generate SQL, execute the query, and return results transparently with sources. User conversations feed back into the system to improve cluster quality over time.

## Key decisions
- Human curation over automated scale: curators accepted only 12.5% of algorithmically generated question-SQL pairs mined from query history, so automated pair generation was rejected. The model reasons over context; experts decide what is true about the data.
- Continuous cluster health scoring — schema validity, pair accuracy, context coverage, SQL reproducibility — to direct curator effort where it matters.
- Closed-loop feedback from real conversations into cluster improvements.
- Multiple integration surfaces so the assistant meets users where they work.

## Stack
LLM-based SQL generation in a ReAct loop; Slack bot, MCP server for IDEs, and web UI as surfaces; execution against the data warehouse.

## Results
Since August 2025: 2,100+ active users, 13,000+ conversations, 60,000+ messages, 177 clusters spanning 8+ domains, and more than 25% of users being non-coders.

## Takeaways
Context curation by domain experts is the foundation of a reliable data assistant, not an implementation detail. Scaling data expertise means amplifying human knowledge through system design rather than replacing judgment with automation — the expert's highest-leverage contribution shifts from answering individual questions to shaping the knowledge layer that serves thousands.
