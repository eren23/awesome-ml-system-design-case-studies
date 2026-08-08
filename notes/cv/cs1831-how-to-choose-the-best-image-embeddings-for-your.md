---
id: cs1831
title: How to Choose the Best Image Embeddings for Your E-commerce Business
company: leboncoin
primary_category: cv
sub_category: visual-search
year: 2025
source_url: https://medium.com/leboncoin-tech-blog/how-to-choose-the-best-image-embeddings-for-your-e-commerce-business-8006f17b495a
tags: [image-embeddings, siglip, convnext, dinov2, visual-search]
---

# How to Choose the Best Image Embeddings for Your E-commerce Business
**leboncoin** · 2025 · [source](https://medium.com/leboncoin-tech-blog/how-to-choose-the-best-image-embeddings-for-your-e-commerce-business-8006f17b495a)

## Problem
For e-commerce visual search and retrieval, choosing the right image embedding model has an outsized impact on quality, but the landscape of supervised, self-supervised, and contrastive models makes comparison difficult. leboncoin needed to select the best embedding approach for its production visual search system across a diverse catalog of secondhand goods.

## Approach / System design
The team conducted a systematic benchmark of multiple embedding model families — supervised models, self-supervised models (DINOv2, ConvNeXt), and contrastive vision-language models (SigLIP) — evaluated across six e-commerce datasets. Models were compared on retrieval quality metrics relevant to visual search. Fine-tuning experiments were run on the top candidates to assess how much domain adaptation improved performance on leboncoin-specific product categories.

## Key decisions
Evaluating across six datasets rather than a single benchmark was essential to ensure findings generalized across product category diversity. SigLIP's contrastive vision-language pretraining gave it an advantage for retrieving semantically similar products even when visual appearance varied. Fine-tuning the best candidate on leboncoin's own catalog data closed the remaining gap between generic model performance and production requirements.

## Stack
SigLIP (contrastive vision-language model, adopted for production), DINOv2, ConvNeXt (evaluated during benchmarking). Specific serving infrastructure details are not covered in the source.

## Results
Fine-tuned SigLIP embeddings outperformed all other evaluated models across the six e-commerce datasets and were selected for production visual search and retrieval. Specific metric values are not covered in the source.

## Takeaways
Contrastive vision-language models like SigLIP can outperform purely visual self-supervised models for e-commerce retrieval by leveraging semantic alignment. Rigorous benchmarking across multiple domain-specific datasets, followed by domain fine-tuning of the best candidate, is a sound approach for embedding model selection in production search systems.
