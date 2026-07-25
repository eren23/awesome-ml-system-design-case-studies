---
id: cs2107
title: "From Facts & Metrics to Media Machine Learning: Evolving the Data Engineering Function at Netflix"
company: Netflix
primary_category: data
sub_category: data-pipeline
year: 2025
source_url: https://netflixtechblog.com/from-facts-metrics-to-media-machine-learning-evolving-the-data-engineering-function-at-netflix-6dcc91058d8d
tags: [media data lake, LanceDB, data engineering, multimodal ML, vector search, embeddings]
---

# From Facts & Metrics to Media Machine Learning: Evolving the Data Engineering Function at Netflix
**Netflix** · 2025 · [source](https://netflixtechblog.com/from-facts-metrics-to-media-machine-learning-evolving-the-data-engineering-function-at-netflix-6dcc91058d8d)

## Problem
Netflix's data engineering discipline grew up building structured fact tables and metrics for dashboards and analytics. Media ML workloads break that mold: video, audio, image, and text assets are unstructured and massive, and ML outputs like embeddings and transcriptions don't fit the classic warehouse pattern. The company needed both a new engineering specialization and new infrastructure to make media assets ML-ready.

## Approach / System design
Netflix created a Media ML Data Engineering specialization and built the Media Data Lake, a platform for storing and serving multimodal media data. Its components:
- **Media Table**: the core structured dataset capturing media asset metadata together with ML model outputs (embeddings, transcriptions).
- **Data API**: a Python interface for programmatic access by ML practitioners.
- **UI components** for visual exploration of media datasets.
- A dual execution model serving both lightweight real-time queries and scalable batch GPU/CPU processing.
Technology-wise, the team integrated LanceDB (vector-native storage) into Netflix's existing Big Data Platform. Rollout was deliberately phased: they started with a "data pond" — a minimal viable version scoped to video/audio datasets sourced from Netflix's internal asset management system (AMP) — to prove the new technology on a solid, extensible foundation before expanding.

## Key decisions
- Recognize media ML data work as a distinct data-engineering specialization rather than stretching the facts-and-metrics model.
- Adopt LanceDB for multimodal/vector storage instead of forcing embeddings into warehouse tables.
- Start with a narrow "data pond" pilot sourced from the canonical asset system, then grow — de-risking new tech adoption.
- Serve both interactive queries and heavy batch ML processing from one platform.

## Stack
LanceDB integrated into Netflix's Big Data Platform; Media Table + Python Data API + exploration UI; AMP (internal asset management) as the source system; GPU/CPU batch processing alongside real-time query paths.

## Results
The platform centralizes media asset access across the organization and provides ML-ready datasets for training and evaluation, powering applications such as translation quality measurement, content understanding, and multimodal search. No quantitative adoption or performance figures were disclosed.

## Takeaways
- Multimodal ML forces data engineering to evolve past tables-and-metrics into serving raw media plus model outputs (embeddings, transcripts) as first-class data.
- Vector-native storage (LanceDB) belongs inside the big data platform, not bolted alongside it.
- "Data pond before data lake" — piloting a minimal scoped version of a new platform is how large orgs adopt unproven technology safely.
