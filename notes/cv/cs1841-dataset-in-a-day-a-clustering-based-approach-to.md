---
id: cs1841
title: Dataset in a Day: A Clustering-Based Approach to Create Image Moderation Datasets
company: Bumble
primary_category: cv
sub_category: image-classification
year: 2023
source_url: https://medium.com/bumble-tech/dataset-in-a-day-7f369de3b178
tags: [content-moderation, clip, clustering, multi-label-classification, resnet50]
---

# Dataset in a Day: A Clustering-Based Approach to Create Image Moderation Datasets
**Bumble** · 2023 · [source](https://medium.com/bumble-tech/dataset-in-a-day-7f369de3b178)

## Problem
Creating labeled training data for image moderation at a social platform is expensive and slow when done through manual annotation. Bumble needed to build multi-label moderation datasets covering lifestyle categories across a large volume of user photos without incurring prohibitive annotation costs or exposing annotators to large volumes of potentially sensitive content.

## Approach / System design
One million user photos are embedded using CLIP and clustered in the resulting embedding space, grouping visually and semantically similar images together. Each cluster is then auto-captioned using the CoCa model, and cluster-level descriptions are summarized in a privacy-preserving way. Human reviewers label clusters rather than individual images, dramatically reducing the annotation burden. The resulting labeled data trains a ResNet50 multi-label classifier across the defined lifestyle moderation categories.

## Key decisions
Using CLIP embeddings for clustering leverages rich semantic representations, grouping images by meaning rather than just low-level visual similarity. Auto-captioning clusters with CoCa before summarization makes cluster review more intuitive for human annotators. Labeling at the cluster level rather than image level is the core efficiency gain, reducing annotation effort by orders of magnitude.

## Stack
CLIP (image embeddings and clustering), CoCa (cluster auto-captioning), ResNet50 (multi-label classifier training). Specific infrastructure details are not covered in the source.

## Results
The approach reduces dataset creation time to approximately one day, versus the multi-week timelines typical of manual per-image annotation campaigns. The cluster-labeling workflow processes approximately 1 million photos.

## Takeaways
Embedding-space clustering is a practical technique for bootstrapping labeled datasets quickly, particularly when the label space can be applied at a cluster granularity. Combining a semantic embedding model (CLIP) with an auto-captioning model (CoCa) makes cluster-level review significantly more tractable for human annotators.
