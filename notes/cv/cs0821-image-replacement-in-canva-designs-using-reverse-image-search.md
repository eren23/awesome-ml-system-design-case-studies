---
id: cs0821
title: Image replacement in Canva designs using reverse image search
company: Canva
primary_category: cv
sub_category: visual-search
year: 2025
source_url: https://www.canva.dev/blog/engineering/image-replacement-in-canva-designs-using-reverse-image-search/
tags: [CV]
---

# Image replacement in Canva designs using reverse image search
**Canva** · 2025 · [source](https://www.canva.dev/blog/engineering/image-replacement-in-canva-designs-using-reverse-image-search/)

## Problem
When a media partnership expires or content becomes unavailable, Canva must swap the affected images across templates with visually similar replacements. Doing this manually across 150M+ images is expensive and slow.

## Approach / System design
Build an image-to-image reverse search using visual embeddings rather than reusing existing systems (recommendation engine, perceptual hashing, text-to-image search), because metadata can't capture nuanced visual features like color, emotion, or secondary subjects. For each image to replace, embed it and find nearest neighbors in an embedding space; surface the top similar candidates to designers in the Template Assistant UI.

## Key decisions
- Visual embeddings over text/metadata representations.
- Model selection by manual evaluation: compared DINOv2, CLIP, ViTMAE, DreamSim, CaiT, plus GPT-4o descriptions, judged by engineers and designers on 200 sample images. DINOv2 best preserved subject, background, and emotional tone.
- Storage: an external vector database (over in-memory) to hold 150M embeddings cost-effectively with real-time updates and metadata filtering (e.g., aspect ratio).
- Faiss used for early testing; a third-party vector DB in production.

## Stack
DINOv2 embeddings; Faiss (prototyping); production vector database; Template Assistant UI surfacing top-8 similar images.

## Results
- ~4.5x faster image-replacement for professional designers.
- Strong on photographs (subject and emotion preserved); weaker on graphics with text, symbols, or cartoons — attributed to DINOv2's photographic training distribution.

## Takeaways
For visual "find a similar replacement" tasks, embedding choice dominates quality, and human side-by-side evaluation is a practical selection method. An external vector DB is the pragmatic store at 100M+ scale when you need updates and metadata filters, and the model's training domain bounds where it works (photos vs graphics).
