---
id: cs1839
title: Spatial: An Evolution in Computing (Decorify for Apple Vision Pro)
company: Wayfair
primary_category: cv
sub_category: visual-search
year: 2024
source_url: https://www.aboutwayfair.com/careers/tech-blog/spatial-an-evolution-in-computing
tags: [generative-ai, diffusion, visual-similarity, augmented-reality, visionos]
---

# Spatial: An Evolution in Computing (Decorify for Apple Vision Pro)
**Wayfair** · 2024 · [source](https://www.aboutwayfair.com/careers/tech-blog/spatial-an-evolution-in-computing)

## Problem
Customers struggle to visualize how furniture and decor will look in their own homes before purchasing. Wayfair's Decorify feature addressed this with room restyling on phones and web, but the arrival of Apple Vision Pro created an opportunity to bring the same capability into a fully spatial, immersive context where the user can view and interact with a restyled version of their real room at scale.

## Approach / System design
Wayfair adapted Decorify for visionOS using diffusion models to regenerate a photo of a room in a new style while preserving the original spatial layout. A visual-similarity matching step then maps objects in the restyled render to shoppable products in the Wayfair catalog, so each element in the generated scene links directly to a purchasable item. The full experience is built for Apple Vision Pro's spatial computing UI paradigm.

## Key decisions
Preserving room layout during diffusion-based restyling was a key constraint: the model must change the aesthetic without repositioning furniture or altering the room's geometry, so the generated image remains a believable representation of the user's actual space. Connecting generated room elements to real catalog products via visual similarity closes the loop between inspiration and purchase.

## Stack
Diffusion models (generative image restyling), visual-similarity search, Wayfair product catalog, Apple Vision Pro, visionOS.

## Results
Not covered in the source.

## Takeaways
Spatial computing hardware opens a new interaction mode for generative shopping experiences, where users can inspect a restyled room at real-world scale rather than on a flat screen. The combination of layout-preserving diffusion and visual-similarity retrieval is a practical architecture for connecting AI-generated imagery to a shoppable catalog.
