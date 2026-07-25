---
id: cs2094
title: Towards LLM-Based Failure Localization in Production-Scale Networks
company: Alibaba Cloud
primary_category: anomaly
sub_category: root-cause
year: 2025
source_url: https://dl.acm.org/doi/10.1145/3718958.3750505
tags: [llm, failure-localization, root-cause, network-operations, alibaba-cloud, production, sigcomm]
---

# Towards LLM-Based Failure Localization in Production-Scale Networks
**Alibaba Cloud** · 2025 · [source](https://dl.acm.org/doi/10.1145/3718958.3750505)

## Problem
Alibaba Cloud runs a global network spanning 87 data centers across 29 regions (as of January 2025). When an incident escapes automated self-healing (roughly 10% of anomalies — about 202 incidents vs. 2,377 self-healed in a typical week), on-call operators must dig through massive monitoring output to find the faulty device. Per-incident alert volume averages 26.4 MB and can exceed 1 GB (~8k log entries), root causes are complex with no fixed investigation recipe, and diagnoses regularly take over 10 minutes — sometimes half an hour — breaching SLAs. Operator capacity, not data availability, was the bottleneck.

## Approach / System design
BiAn is an LLM-agent framework that assists (not replaces) operators by turning raw monitor alerts into a ranked list of candidate error devices with explanations. Design pillars:
- **Hierarchical reasoning**: instead of feeding everything to one model, BiAn (1) summarizes alerts from 11 upstream monitoring tools via dedicated per-alert-type LLM agents, (2) runs device-level anomaly analysis following SOPs distilled from operators' years of incident handling — anomalies map to 7 scenarios defined from 10 years of operational experience that cover 100% of alert-observable incidents, and (3) jointly scores devices to produce suspicion-ranked candidates.
- **Multi-pipeline integration**: adds network topology (spatial) and event timeline (temporal) pipelines alongside alert processing to handle failures that propagate across logically nearby devices.
- **Continuous updating**: LLM-driven generation/reflection/summarization extracts knowledge from historical incidents into a digest that enriches task prompts, keeping pace with network evolution.
- **Practical optimizations**: smaller fine-tuned LLMs for simpler tasks (alert summary, single-device analysis), an early-stop mechanism when confidence is already high after the first stage, and parallel execution of same-level agents for real-time latency.

## Key decisions
- Position the system as an operator assistant producing ranked candidates plus explanations — fault-tolerant (operators check secondary devices if the top pick is wrong) and trustable, versus opaque one-shot answers.
- Process each alert type with its own carefully prompted agent (role definition, input field description, guidelines, examples, expected output format), making it easy to extend to new monitors by adding agents.
- Use LLM reasoning as a bridge over traditional heuristic/statistical tools, which generalize poorly to unseen incidents; prior LLM-for-networking work was either coarse-grained or relied on lossy incident summaries.
- Constrain single-device analysis to the operator-defined 7-scenario taxonomy to simplify and stabilize reasoning.

## Stack
LLM agents with crafted prompt templates and fine-tuned smaller models for sub-tasks; inputs from 11 production monitoring tools (device ping logs, traffic stats, etc.); topology and event-timeline data pipelines; deployed inside Alibaba Cloud's network operations center workflow.

## Results
- Deployed in the global production network for ~10 months at publication.
- Reduced time-to-root-cause by 20.5% overall, and 55.2% for high-risk incidents.
- Improved localization accuracy by 9.2% over the baseline approach.
- Validated with A/B tests, operator feedback, representative real cases, and offline experiments over 17 months of real incident data.

## Takeaways
- Hierarchical decomposition (summarize → per-device analysis → joint scoring) is how you get LLMs to cope with 1 GB-scale incident telemetry that neither humans nor single context windows can absorb.
- Encoding veteran operators' SOPs and a small closed set of anomaly scenarios grounds LLM reasoning and covers the practical incident space.
- Ranked, explained outputs keep humans in the loop and make LLM randomness survivable in high-stakes operations.
- Continuous prompt "training" from historical incidents is needed because production networks evolve too fast for static knowledge.
