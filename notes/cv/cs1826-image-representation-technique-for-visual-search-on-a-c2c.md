---
id: cs1826
title: Image Representation Technique for Visual Search on a C2C Marketplace
company: Mercari
primary_category: cv
sub_category: visual-search
year: 2019
source_url: https://medium.com/mercari-engineering/image-representation-technique-for-visual-search-on-a-c2c-marketplace-1fc27ee59ede
tags: [visual-search, mobilenet, image-retrieval, ivfadc, apparel]
---

# Image Representation Technique for Visual Search on a C2C Marketplace
**Mercari** · 2019 · [source](https://medium.com/mercari-engineering/image-representation-technique-for-visual-search-on-a-c2c-marketplace-1fc27ee59ede)

## Problem
Visual search on a C2C marketplace faces a domain-specific challenge: apparel items are photographed both on a person (fitted) and laid flat, producing dramatically different image appearances for the same type of item. This distribution mismatch causes naive embedding models to fail at matching a fitted photo to a flat photo of a similar garment, degrading retrieval quality for apparel categories.

## Approach / System design
MobileNetV2 is used as the base embedding model to produce compact, efficient image representations. To handle the fitted-vs-flat appearance gap in apparel, the team learns a "gap vector" — a vector transform applied to embeddings — that bridges the two photographic styles so that visually similar items retrieve across the style divide. Over 100 million listing images are indexed for retrieval using IVFADC, an inverted-file approximate nearest-neighbor method that combines coarse quantization with product quantization for compact, fast retrieval at scale.

## Key decisions
MobileNetV2 was chosen for its efficiency, making it feasible to embed and serve over 100 million listings. The learned gap vector is a lightweight domain-adaptation technique that specifically targets the fitted/flat apparel mismatch without requiring a full model retraining cycle. IVFADC was selected because it supports sub-linear approximate nearest-neighbor search at the scale of 100M+ images with manageable memory usage.

## Stack
MobileNetV2 (image embedding), learned gap vector (domain adaptation transform), IVFADC (approximate nearest-neighbor indexing over 100M+ images).

## Results
The system indexes over 100 million listing images and supports production visual search. Specific retrieval accuracy or latency metrics are not covered in the source.

## Takeaways
Domain-specific appearance variation — such as fitted vs. flat apparel photography — requires explicit modeling beyond a generic embedding model; a learned gap vector is a lightweight fix for this. Scalable approximate nearest-neighbor indexing like IVFADC is essential when the retrieval corpus reaches hundreds of millions of items.
