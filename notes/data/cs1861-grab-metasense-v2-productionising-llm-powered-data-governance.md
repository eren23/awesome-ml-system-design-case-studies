---
id: cs1861
title: "Grab — Metasense V2: Productionising LLM-Powered Data Governance"
company: Grab
primary_category: data
sub_category: data-discovery
year: 2024
source_url: https://engineering.grab.com/metasense-v2
tags: [data-governance, llm, data-classification, pii, langchain, metadata]
---

# Grab — Metasense V2: Productionising LLM-Powered Data Governance
**Grab** · 2024 · [source](https://engineering.grab.com/metasense-v2)

## Problem
Grab's data lake contains a large and growing number of datasets with sensitive attributes — including personally identifiable information — that must be discovered, tagged, and governed to meet regulatory and internal privacy requirements. Manual tagging at scale is impractical, and the first version of the Metasense system needed maturation to handle production reliability, classification accuracy, and operational monitoring.

## Approach / System design
Metasense V2 splits the LLM-based classification into two specialized models: one focused on PII detection and one on non-PII metadata classification. Prompts for each model were optimized separately based on observed failure modes. The system is built on LangChain for LLM orchestration and uses LangSmith for tracing, evaluation, and debugging. A misclassification monitoring layer was added to detect and alert on cases where the model's output diverges from expected or validated labels, enabling continuous quality feedback.

## Key decisions
Splitting PII and non-PII classification into separate models allowed each to be optimized for its specific label distribution and sensitivity requirements without the two tasks interfering with each other. Adopting LangSmith alongside LangChain was a deliberate choice to gain observability into LLM calls at the step level, which is essential for debugging production classification errors. Misclassification monitoring closes the feedback loop between production behavior and model improvement.

## Stack
LangChain (LLM orchestration), LangSmith (tracing and evaluation), LLM (classification), internal data lake and metadata store.

## Results
Not covered in the source.

## Takeaways
Productionising LLM-based classification requires more than a working prompt: it demands task decomposition, prompt optimization, observability tooling, and ongoing monitoring of output quality. Splitting a broad classification task into narrower subtasks with dedicated models is a practical way to improve accuracy and manageability at scale.
