---
id: cs1829
title: "Making the Best First Impression: Using Machine Learning to Optimize Photo Selection"
company: Tripadvisor
primary_category: cv
sub_category: image-classification
year: 2025
source_url: https://medium.com/tripadvisor/making-the-best-first-impression-using-machine-learning-to-optimize-photo-selection-0767e82e4fe8
tags: [photo-ranking, siamese-network, ranknet, llm-labeling, image-aesthetics]
---

# Making the Best First Impression: Using Machine Learning to Optimize Photo Selection
**Tripadvisor** · 2025 · [source](https://medium.com/tripadvisor/making-the-best-first-impression-using-machine-learning-to-optimize-photo-selection-0767e82e4fe8)

## Problem
Tripadvisor listings each have many user-contributed photos, and the cover image a visitor sees first has a significant effect on click-through and engagement. Selecting the single best photo from potentially hundreds of candidates manually is not feasible at the scale of millions of listings, and simple heuristics (recency, upload count) do not reliably pick the most visually appealing image.

## Approach / System design
Tripadvisor built a Primary Photo Service around a Siamese pairwise ranking model trained in a RankNet-style setup. Rather than relying on expensive human annotation, preference labels were generated at scale using an LLM. The model learns to score photos relative to each other; the highest-ranked photo for each listing is selected as the cover image. A dedicated serving layer handles the request volume at peak traffic.

## Key decisions
Using an LLM to generate pairwise preference labels removed the bottleneck of human labeling and allowed training on a much larger dataset than would otherwise be practical. A pairwise (RankNet) formulation was preferred over pointwise scoring because it captures relative attractiveness rather than requiring an absolute quality scale, which is inherently subjective.

## Stack
Siamese neural network, RankNet-style pairwise training, LLM-generated preference labels, dedicated serving infrastructure.

## Results
The service handles approximately 12,000 requests per second at peak load, covering the full Tripadvisor listing catalog in near real time.

## Takeaways
Combining LLM-generated labels with pairwise ranking models is an effective way to build large-scale aesthetic ranking systems without expensive human annotation pipelines. High-throughput serving of image ranking at this scale requires dedicated infrastructure separate from general-purpose ML serving.
