---
id: cs1830
title: Introducing Image Search & Price Suggestions
company: Carousell
primary_category: cv
sub_category: visual-search
year: 2019
source_url: https://medium.com/carousell-insider/introducing-image-search-price-suggestions-ce8e40a0163f
tags: [visual-search, joint-embeddings, annoy, approximate-nearest-neighbor, price-suggestion]
---

# Introducing Image Search & Price Suggestions
**Carousell** · 2019 · [source](https://medium.com/carousell-insider/introducing-image-search-price-suggestions-ce8e40a0163f)

## Problem
Carousell users often have an item they want to sell but lack the words to describe it or find comparable listings, making search and pricing difficult. A purely text-based search also fails when users want to find visually similar items. Carousell needed to let users search by photo and automatically suggest a reasonable price based on visual similarity to existing listings.

## Approach / System design
A CNN is trained to embed both listing images and listing titles into a shared vector space, producing joint image-text embeddings where visually and semantically similar items cluster together. At query time, a user's photo is embedded by the same model and nearest neighbors are retrieved from the listing index. Spotify's Annoy library handles the approximate nearest-neighbor (ANN) search to make retrieval fast over a large index. Price suggestions are derived from the prices of the retrieved similar listings.

## Key decisions
Mapping images and text into a joint embedding space allows the same index to support both visual similarity search and cross-modal retrieval. Annoy was selected for ANN retrieval because of its favorable speed-accuracy tradeoff and low memory footprint at the time. Grounding price suggestions in visually similar listings rather than a separate pricing model keeps the approach simple and interpretable.

## Stack
CNN for joint image-text embeddings, Annoy (approximate nearest-neighbor indexing and retrieval). Specific training infrastructure details are not covered in the source.

## Results
Not covered in the source.

## Takeaways
Joint embedding spaces that bridge image and text modalities can power multiple features (visual search and price suggestion) from a single model and index. Approximate nearest-neighbor libraries like Annoy make large-scale similarity retrieval practical without requiring specialized vector database infrastructure.
