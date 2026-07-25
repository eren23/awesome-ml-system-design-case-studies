---
id: cs2377
title: "See the Similarity: Personalizing Visual Search with Multimodal Embeddings"
company: Google
primary_category: cv
sub_category: visual-search
year: 2024
source_url: https://developers.googleblog.com/en/see-the-similarity-personalizing-visual-search-with-multimodal-embeddings/
tags: [visual-search, multimodal-embeddings, personalization, image-retrieval]
---

# See the Similarity: Personalizing Visual Search with Multimodal Embeddings
**Google** · 2024 · [source](https://developers.googleblog.com/en/see-the-similarity-personalizing-visual-search-with-multimodal-embeddings/)

## Problem
Artists and large organizations struggle to find past visual work by similarity or concept — traditional file organization fails when searching by uncommon terms, abstract ideas, or "looks like this" queries, whether over a personal illustration collection or a corporate archive of hundreds of thousands of slides.

## Approach / System design
Two demonstrations built on Google's Multimodal Embeddings API, which maps text, images, and video into a shared 1408-dimensional vector space:
1. **Artist demo**: a Svelte app letting a designer search their illustration collection (~250 images) semantically, backed by Firebase with Firestore Vector Search using K-nearest neighbors.
2. **Enterprise demo**: a search system over a large presentation archive (775,000+ slides across 16,000+ presentations), pulling content via Google Drive and Slides APIs and indexing with Vertex AI Vector Search using ScaNN approximate nearest neighbor.
They also tested sqlite-vec as a local, zero-dependency vector store alternative.

## Key decisions
- Pick the vector store by scale: Firestore Vector Search (exact KNN) is cost-effective for small collections; Vertex AI Vector Search (ScaNN) is needed for enterprise-scale latency.
- Use one shared embedding space for text and images so users can query visually or with free-text concepts interchangeably.
- Offer a local option (sqlite-vec) for cases where cloud infrastructure isn't warranted.

## Stack
Google Multimodal Embeddings API (1408-dim), Firebase/Firestore Vector Search (KNN), Vertex AI Vector Search (ScaNN), Google Drive and Slides APIs, sqlite-vec, Svelte frontend.

## Results
- Enterprise index: 775,000+ slides from 16,000+ presentations made semantically searchable.
- Vertex AI: ~100ms vector lookup plus ~50ms metadata retrieval, versus notably slower Firestore performance at that scale; sqlite-vec managed ~200ms lookups locally.
- Artist collection of ~250 illustrations searchable by concept and similarity.

## Takeaways
Multimodal embeddings turn visual archives into semantically searchable assets with little bespoke ML work — the engineering decision that matters is matching the vector search backend to dataset size, since exact KNN that is fine at hundreds of items breaks down at hundreds of thousands, where ScaNN-style approximate search keeps lookups in the millisecond range.
