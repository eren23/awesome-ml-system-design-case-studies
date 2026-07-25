---
id: cs2324
title: Bringing Multimodality to Amazon Visual Search System
company: Amazon
primary_category: cv
sub_category: visual-search
year: 2023
source_url: https://www.amazon.science/publications/bringing-multimodality-to-amazon-visual-search-system
tags: [vlm, visual-search, multimodal, ecommerce, embeddings, text-image]
---

# Bringing Multimodality to Amazon Visual Search System
**Amazon** · 2023 · [source](https://www.amazon.science/publications/bringing-multimodality-to-amazon-visual-search-system)

## Problem
Amazon's visual search relied on pure image-to-image matching via deep metric learning, which produced false positives: the model would match low-level visual patterns (texture, color, layout) rather than the semantic content of the product. The team needed to raise relevance and also support queries that mix an image with textual intent.

## Approach / System design
The team progressively extended the image-matching model with vision-language alignment:
- **3-tower model**: keeps the image-to-image deep metric learning objective but adds image-text alignment losses (in the style of vision-language pretraining), using text from product titles and query reformulations. The extra alignment constrains the embedding space so the model learns concepts shared across modalities instead of superficial visual similarity.
- **4-tower model**: adds a short text-query input tower on top, enabling true multimodal search where a user's image can be combined with a text refinement, with multimodal fusion producing the retrieval embedding.
Both variants were validated offline and in online experiments before deployment in the production visual search system with real-time inference.

## Key decisions
- Treat text alignment as a regularizer on the visual embedding space rather than replacing the image-matching objective — the alignment losses explicitly push the model away from matching low-level visual features.
- Evolve the architecture incrementally (3-tower first, then 4-tower) so each addition could be measured against the production baseline.
- Source paired text from existing signals (product titles, query reformulations) rather than new annotation.

## Stack
Deep metric learning framework, vision-language pretraining-style alignment losses, multi-tower embedding architecture (3- and 4-tower), multimodal image+text embedding space, real-time inference serving. Specific model backbones and infrastructure are not named in the source.

## Results
- 3-tower model: 4.95% relative improvement in image-matching click-through rate over the production baseline.
- 4-tower model: a further 1.13% improvement over the 3-tower model, while adding text-query capability.
- Improvements held in both offline evaluation and online experiments.

## Takeaways
- Adding language supervision to a visual retrieval model is an effective cure for low-level-pattern false positives: text forces the embedding to encode semantics.
- Multimodal (image + text) query support can be layered onto an existing visual search system rather than requiring a rebuild.
- Incremental tower-by-tower evolution lets a production team attribute gains to each architectural change.
