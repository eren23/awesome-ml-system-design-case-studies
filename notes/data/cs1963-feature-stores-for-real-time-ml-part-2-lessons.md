---
id: cs1963
title: Feature stores for real-time ML: Part 2 - Lessons learned from production
company: Nubank
primary_category: data
sub_category: feature-store
year: 2026
source_url: https://building.nubank.com/feature-stores-for-real-time-ml-part-2-lessons-learned-from-production/
tags: [feature-store, real-time-ml, streaming, kafka, training-serving-skew]
---

# Feature stores for real-time ML: Part 2 - Lessons learned from production
**Nubank** · 2026 · [source](https://building.nubank.com/feature-stores-for-real-time-ml-part-2-lessons-learned-from-production/)

## Problem
Running a real-time feature store in production exposes challenges that are not visible during initial design: naming inconsistencies across teams, training-serving skew caused by different feature computation paths, and the operational complexity of maintaining streaming infrastructure at scale. Without deliberate governance, a feature store becomes a fragmented collection of pipelines rather than a shared platform.

## Approach / System design
Nubank treats its real-time feature store as an internal product rather than a shared infrastructure component. The platform is built on a hybrid build-vs-buy approach running on Kubernetes with Kafka for event streaming, Apache Flink for stateful stream processing, and Apache Pinot for low-latency analytical reads. Streaming-first feature retrieval is the default, and train-serve skew is monitored explicitly by comparing online and offline feature distributions.

## Key decisions
Adopting strict naming conventions across all feature definitions reduced confusion and made the catalog easier to navigate as the number of features grew. Prioritizing streaming-first retrieval rather than batch-first ensured that the freshest features were available to online models by default, with batch as a fallback.

## Stack
Kubernetes, Apache Kafka, Apache Flink, Apache Pinot.

## Results
Not covered in the source.

## Takeaways
Treating a feature store as an internal product—with versioning, naming standards, and an owner team accountable for adoption—is more effective than deploying it as neutral infrastructure and expecting organic uptake. Continuous monitoring of train-serve skew is essential in a real-time setting because subtle differences in feature computation between training and serving pipelines compound into model degradation over time.
