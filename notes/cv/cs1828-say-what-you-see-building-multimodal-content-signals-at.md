---
id: cs1828
title: Say What You See: Building Multimodal Content Signals at Scale
company: Agoda
primary_category: cv
sub_category: vlm
year: 2026
source_url: https://medium.com/agoda-engineering/say-what-you-see-building-multimodal-content-signals-at-scale-0fa5ee20a02b
tags: [multimodal, image-tagging, topic-clustering, pyspark, kubeflow]
---

# Say What You See: Building Multimodal Content Signals at Scale
**Agoda** · 2026 · [source](https://medium.com/agoda-engineering/say-what-you-see-building-multimodal-content-signals-at-scale-0fa5ee20a02b)

## Problem
Agoda has over 700 million hotel images and a large corpus of multilingual guest reviews, but these two content modalities were managed separately with no shared semantic structure. Without a unified topic taxonomy bridging images and text, the app could not surface coherent multimodal highlights to users searching for specific experiences or property features.

## Approach / System design
The team built image classification and NLP pipelines that map both visual and textual content into a shared topic taxonomy. Image classifiers assign topic labels to hotel photos, while NLP models extract topic signals from multilingual reviews. PySpark handles large-scale batch processing of both modalities, and Kubeflow orchestrates the end-to-end ML pipelines. The aligned topic signals are then surfaced as multimodal highlights in the app.

## Key decisions
Creating a shared topic taxonomy was the foundational design decision, requiring alignment between the image classification label space and NLP topic extraction. PySpark was chosen to scale processing across hundreds of millions of images and reviews. Kubeflow provided the pipeline orchestration needed to manage multi-step ML workflows reliably.

## Stack
Image classification models, NLP topic extraction models, PySpark (distributed batch processing), Kubeflow (ML pipeline orchestration).

## Results
Multimodal highlights in the app saw a doubling of user clicks after the feature launched. The system processes over 700 million hotel images alongside multilingual review content.

## Takeaways
Aligning image and text signals into a shared topic taxonomy enables new product experiences that neither modality could support alone. Doubling click-through rates on highlights demonstrates that multimodal content signals have measurable business impact at scale.
