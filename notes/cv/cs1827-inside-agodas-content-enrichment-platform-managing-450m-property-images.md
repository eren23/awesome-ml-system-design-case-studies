---
id: cs1827
title: Inside Agoda's Content Enrichment Platform: Managing 450M+ Property Images
company: Agoda
primary_category: cv
sub_category: image-classification
year: 2025
source_url: https://medium.com/agoda-engineering/inside-agodas-content-enrichment-platform-managing-450m-property-images-516bf4bee165
tags: [image-tagging, deduplication, super-resolution, vision-transformer, spark]
---

# Inside Agoda's Content Enrichment Platform: Managing 450M+ Property Images
**Agoda** · 2025 · [source](https://medium.com/agoda-engineering/inside-agodas-content-enrichment-platform-managing-450m-property-images-516bf4bee165)

## Problem
Agoda manages over 450 million property images that need to be automatically enriched with quality scores, semantic tags, and deduplicated, so that only the best and most relevant images surface to users. The existing metadata replication process was slow, taking days to propagate updates across the platform, which prevented timely quality improvements.

## Approach / System design
The Content Enrichment Platform chains four ML capabilities: a DenseNet169-based model scores image quality, a Vision Transformer assigns semantic tags, RealESRGAN upscales lower-resolution images via super-resolution, and cosine-similarity-based deduplication removes near-duplicate photos. The entire batch processing pipeline is orchestrated on Apache Spark, with Couchbase serving as the metadata store for enriched image attributes.

## Key decisions
DenseNet169 was chosen for quality scoring and ViT for tagging, reflecting a deliberate move toward transformer-based vision models for richer semantic understanding. RealESRGAN super-resolution was integrated to improve the visual quality of images that would otherwise be discarded due to low resolution. Using Spark for distributed batch processing was essential to handle the 450M+ image scale.

## Stack
DenseNet169 (quality scoring), Vision Transformer (image tagging), RealESRGAN (super-resolution), cosine similarity (deduplication), Apache Spark (batch orchestration), Couchbase (metadata store).

## Results
Metadata replication time dropped from days to approximately 20 minutes after the platform rebuild. The pipeline processes over 450 million property images.

## Takeaways
Combining quality scoring, tagging, super-resolution, and deduplication in a unified enrichment pipeline greatly reduces the operational complexity of managing a large-scale image catalog. Reducing metadata propagation latency from days to minutes has direct product impact by enabling faster content quality improvements.
