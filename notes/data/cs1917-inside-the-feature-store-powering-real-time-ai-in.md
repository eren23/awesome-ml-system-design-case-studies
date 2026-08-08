---
id: cs1917
title: Inside the feature store powering real-time AI in Dropbox Dash
company: Dropbox
primary_category: data
sub_category: feature-store
year: 2025
source_url: https://dropbox.tech/machine-learning/feature-store-powering-realtime-ai-in-dropbox-dash
tags: [feature-store, rag, low-latency, ranking, feast]
---

# Inside the feature store powering real-time AI in Dropbox Dash
**Dropbox** · 2025 · [source](https://dropbox.tech/machine-learning/feature-store-powering-realtime-ai-in-dropbox-dash)

## Problem
Dropbox Dash is a real-time AI search and productivity product that requires low-latency feature retrieval to power its ranking models. The initial Python-based serving layer introduced too much overhead to meet latency targets, and co-locating feature storage with the inference service was needed to avoid network round-trip costs.

## Approach / System design
Dropbox built a hybrid feature store on top of Feast, combining offline and online feature pipelines. The online serving path was rewritten from Python to Go to reduce per-request overhead. Feature storage uses an in-house system called Dynovault, deployed co-located with the inference service to minimize the latency of feature retrieval during ranking. The hybrid design allows features to be computed both from streaming and batch sources, depending on their freshness requirements.

## Key decisions
Rewriting the serving layer in Go rather than continuing to optimize the Python implementation was a deliberate trade-off: the performance gain justified the additional engineering effort given strict latency SLOs. Co-locating Dynovault with inference rather than using a remote feature store eliminated a network hop that would otherwise dominate p95 latency. Feast was chosen as the framework to provide structure and tooling without requiring a full from-scratch build.

## Stack
Feast (feature store framework), Go (serving layer), Python (feature engineering), Dynovault (in-house online storage), Dropbox Dash inference infrastructure.

## Results
The rewritten serving layer achieved approximately 25–35 ms at p95 latency for feature retrieval.

## Takeaways
For latency-sensitive feature serving, language runtime overhead and network topology are the dominant factors; switching from Python to Go and co-locating storage with inference yielded the largest gains. Building on an open-source framework like Feast while customizing the serving layer allows teams to get the benefits of community tooling without being constrained by its performance defaults.
