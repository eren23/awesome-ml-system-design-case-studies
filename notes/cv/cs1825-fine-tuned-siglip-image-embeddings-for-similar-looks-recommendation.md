---
id: cs1825
title: Fine-tuned SigLIP Image Embeddings for Similar Looks Recommendation in a Japanese C2C Marketplace
company: Mercari
primary_category: cv
sub_category: vlm
year: 2024
source_url: https://engineering.mercari.com/en/blog/entry/20241104-similar-looks-recommendation-via-vision-language-model/
tags: [image-embeddings, siglip, vision-language, visual-recommendation, tensorrt]
---

# Fine-tuned SigLIP Image Embeddings for Similar Looks Recommendation in a Japanese C2C Marketplace
**Mercari** · 2024 · [source](https://engineering.mercari.com/en/blog/entry/20241104-similar-looks-recommendation-via-vision-language-model/)

## Problem
Mercari's C2C marketplace needed a "Similar Looks" recommendation feature that could surface visually comparable listings to users browsing items. The challenge was that a generic vision model would not understand the specific visual vocabulary and style signals relevant to Mercari's Japanese secondhand goods catalog, and inference latency had to be acceptable for a recommendation use case at scale.

## Approach / System design
The team fine-tuned a multilingual SigLIP vision-language model on approximately 1 million image-title pairs sourced from Mercari's own listings, teaching the model to associate the visual appearance of items with their marketplace-specific text descriptions. The fine-tuned model produces image embeddings that capture Mercari-relevant visual signals. The model is then converted to TensorRT for GPU-accelerated inference, and the resulting service is deployed on Google Kubernetes Engine (GKE) to serve "Similar Looks" recommendations.

## Key decisions
Using SigLIP's vision-language architecture allowed the model to leverage text supervision from listing titles during fine-tuning, which is richer signal than image-only contrastive learning. The ~1M image-title pair fine-tuning set was drawn from actual Mercari listings to ensure domain relevance. TensorRT conversion was essential to make inference fast enough for production recommendation serving.

## Stack
Multilingual SigLIP (vision-language model), fine-tuning on ~1M Mercari image-title pairs, TensorRT (inference optimization), Google Kubernetes Engine (GKE, serving).

## Results
TensorRT conversion delivers approximately 5x faster inference compared to the baseline model. The feature achieved a tap rate improvement of approximately 1.5x after launch.

## Takeaways
Fine-tuning a vision-language model on marketplace-specific image-title pairs is an effective way to adapt a general-purpose embedding model to the visual vocabulary of a specific product domain. Combining domain fine-tuning with compiler-level inference optimization (TensorRT) is necessary to bridge the gap between research model quality and production latency requirements.
