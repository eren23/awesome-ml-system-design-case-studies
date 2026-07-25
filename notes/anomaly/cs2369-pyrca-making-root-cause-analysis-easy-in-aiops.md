---
id: cs2369
title: "PyRCA: Making Root Cause Analysis Easy in AIOps"
company: Salesforce
primary_category: anomaly
sub_category: root-cause
year: 2023
source_url: https://www.salesforce.com/blog/pyrca/
tags: [root-cause-analysis, causal-inference, AIOps, open-source, IT-operations, microservices]
---

# PyRCA: Making Root Cause Analysis Easy in AIOps
**Salesforce** · 2023 · [source](https://www.salesforce.com/blog/pyrca/)

## Problem
Cloud systems are monitored via KPI metrics, and anomalies in those KPIs are treated as incidents. Modern systems comprise many services with complex, distributed dependencies, so an incident can implicate thousands of potentially relevant metrics. Manually walking upstream dependencies (e.g., tracing a slow web service back to a slow database) is time-consuming, labor-intensive, and error-prone — engineers need automated root cause analysis (RCA).

## Approach / System design
PyRCA is an open-source Python library providing an end-to-end RCA framework: data loading, causal graph discovery, root cause localization, and results visualization. In a production integration, the monitoring system streams service metrics; when the anomaly detection module flags anomalous metrics, it triggers the RCA module, which builds a causal graph from metrics plus expert knowledge, computes root cause scores over the graph, and surfaces the top-K likely root-cause metrics to SREs for remediation. The API has three layers: an input layer (metric data as pandas DataFrames, expert knowledge as YAML config), a model layer (anomaly detection, causal graph construction, and root cause scoring models behind a unified interface), and an output layer (causal graph visualization and RCA evaluation). A GUI dashboard supports interactive RCA without coding.

## Key decisions
- Framed RCA as causal-graph construction plus root-cause scoring, rather than ad-hoc metric correlation.
- Unified interface over multiple RCA models so users can benchmark and swap approaches; new models are added by inheriting one base class.
- First-class support for injecting user-provided domain knowledge (YAML), making models more robust to noisy metric data.
- Shipped a no-code visualization dashboard because interactive expert-in-the-loop RCA matches real-world usage.

## Stack
Python; pandas DataFrames for metric input; YAML for expert-knowledge configuration; a built-in GUI dashboard; open-sourced by Salesforce AI Research.

## Results
Not covered in the source — the post describes the library's design and capabilities rather than quantitative production outcomes.

## Takeaways
Automating RCA in AIOps means combining statistical causal discovery with human domain knowledge; neither alone handles noisy production metrics well. A standardized framework with a unified model interface lets operators, data scientists, and researchers develop, evaluate, and deploy RCA models quickly, and an interactive dashboard is essential because RCA in practice is a collaborative, iterative workflow.
