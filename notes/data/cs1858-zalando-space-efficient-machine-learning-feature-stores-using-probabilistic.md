---
id: cs1858
title: Zalando — Space Efficient Machine Learning Feature Stores Using Probabilistic Data Structures
company: Zalando
primary_category: data
sub_category: feature-store
year: 2021
source_url: https://engineering.zalando.com/posts/2021/10/space-efficient-machine-learning-feature-stores-using-probabilistic-data-structures.html
tags: [feature-store, bloom-filter, probabilistic-data-structures, in-memory, benchmark]
---

# Zalando — Space Efficient Machine Learning Feature Stores Using Probabilistic Data Structures
**Zalando** · 2021 · [source](https://engineering.zalando.com/posts/2021/10/space-efficient-machine-learning-feature-stores-using-probabilistic-data-structures.html)

## Problem
Serving machine learning features at low latency typically requires an external key-value store such as Redis, which carries significant infrastructure cost and memory overhead. Zalando investigated whether probabilistic data structures could store feature data directly in process memory without meaningful accuracy loss.

## Approach / System design
The team benchmarked bloom filters as an in-process, compressed replacement for a conventional external feature store. Feature membership and approximate values are encoded in the probabilistic structure, allowing the serving layer to answer feature lookups without a network round-trip to Redis or a similar store.

## Key decisions
Trading exact key-value accuracy for a dramatic reduction in memory footprint was the central design choice. The benchmark explicitly quantified the accuracy trade-off (AUC) alongside the space savings so that downstream teams could make an informed decision about whether the loss was acceptable for a given use case.

## Stack
Bloom filters (probabilistic data structures), in-memory serving, benchmarked against a Redis-style external key-value store.

## Results
The bloom-filter approach matched conventional key-value accuracy at approximately AUC ~0.80 while consuming roughly 3% of the memory required by the external store, representing a very large reduction in memory usage.

## Takeaways
Probabilistic data structures can be a practical option for feature serving when the application can tolerate a small, well-characterised accuracy trade-off. The memory savings are substantial enough to eliminate the need for an external store in many scenarios, but teams must benchmark the specific accuracy impact for their model before adopting this approach.
