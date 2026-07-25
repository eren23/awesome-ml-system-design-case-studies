---
id: cs2401
title: "Introducing FBLearner Flow: Facebook's AI backbone"
company: Meta
primary_category: mlops
sub_category: platform
year: 2016
source_url: https://engineering.fb.com/ml-applications/introducing-fblearner-flow-facebook-s-ai-backbone/
tags: [ml platform, workflow management, model training, feature engineering, model serving, internal platform, distributed training]
---

# Introducing FBLearner Flow: Facebook's AI backbone
**Meta** · 2016 · [source](https://engineering.fb.com/ml-applications/introducing-fblearner-flow-facebook-s-ai-backbone/)

## Problem
Facebook wanted ML in the hands of every engineer, not just ML specialists — but engineers without ML backgrounds couldn't effectively use the existing infrastructure. The team also observed that the biggest accuracy wins came from quick experiments, feature engineering, and model tuning rather than fundamentally new algorithms, so the platform had to optimize for rapid iteration.

## Approach / System design
FBLearner Flow executes ML workflows in two stages. First, a **DAG compilation stage**: workflows are written in Python but return futures (delayed computations) instead of executing immediately, letting the system build a dependency DAG. Second, an **operator execution stage**: a scheduler runs each operator as soon as its dependencies complete, giving implicit parallelism across independent tasks. The platform comprises three components: a workflow authorship/execution environment, an experimentation-management UI, and a library of predefined pipelines for common algorithms.

## Key decisions
- Python-based workflow definitions with decorators providing type safety and automatic input validation.
- A custom type system whose schemas drive automatic UI generation for launching and inspecting workflows.
- Futures-based dataflow to get distributed, parallel execution without users writing orchestration code.
- Elasticsearch indexing of every run so experiments are searchable and comparable across the company.

## Stack
Python (workflow DSL), Hive (data warehouse), a custom type system, Elasticsearch (experiment index).

## Results
- Used by more than 25% of Facebook's engineering team, while fewer than 150 people had authored workflows — reuse at organizational scale.
- Over 1 million models trained since inception.
- 500,000+ workflow runs executed per month (as of April 2016).
- Deployed models serving over 6 million predictions per second.

## Takeaways
- Abstracting infrastructure behind declarative workflow definitions and auto-generated UIs is what democratizes ML across an engineering org.
- A small number of workflow authors can serve a very large consumer base if pipelines are reusable and discoverable.
- Optimizing the platform for experiment velocity (not novel algorithms) is where the accuracy gains actually come from.
