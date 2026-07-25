---
id: cs2327
title: Introducing the Future of Visual Discovery on Pinterest
company: Pinterest
primary_category: cv
sub_category: image-classification
year: 2022
source_url: https://medium.com/pinterest-engineering/introducing-the-future-of-visual-discovery-on-pinterest-48fb469b0d67
tags: [visual-search, embeddings, recommendations, image-classification, retrieval]
---

# Introducing the Future of Visual Discovery on Pinterest
**Pinterest** · 2022 · [source](https://medium.com/pinterest-engineering/introducing-the-future-of-visual-discovery-on-pinterest-48fb469b0d67)

## Problem
Text queries fail when people can't put what they see into words. Pinterest — a visual discovery engine with 100B ideas saved by 150M people — had shipped visual search (2015) and real-time object detection (2016), but wanted any image, whether on Pinterest or in the physical world, to become an entry point into discovery, shopping, and personalized recommendations.

## Approach / System design
Three products launched on top of Pinterest's shared visual discovery infrastructure:
- **Lens (beta)**: camera-based discovery on iOS and Android. Users photograph anything — shoes, produce, furniture — and Lens returns not just visually similar items but semantically useful results: recipes for photographed strawberries, outfit ideas featuring a spotted sneaker style. It builds on the prior year's computer vision and machine learning advances to infer what an object is and how it could be useful.
- **Shop the Look**: shoppable results for products inside Pins, combining computer vision with human curation to recommend related products and styles purchasable on Pinterest or from brands, including styling ideas for Buyable Pins.
- **Instant Ideas**: a one-tap control on any home-feed Pin that fetches similar ideas, built on the machine learning stack that powers 10B daily recommendations; the tap signals feed real-time personalization of the home feed.
The underlying visual search system had by this point become one of Pinterest's most-used features, serving hundreds of millions of visual searches monthly and detecting billions of objects.

## Key decisions
- Build all three products on one shared visual discovery infrastructure rather than per-product vision stacks.
- Push beyond visual similarity toward intent understanding — returning recipes, outfits, and use-cases, not just lookalike images.
- Blend computer vision with human curation for the shopping experience (Shop the Look) where precision matters commercially.
- Use lightweight in-feed interaction signals (Instant Ideas taps) to drive real-time feed personalization.
- Ship Lens as a beta designed to improve as more people use it.

## Stack
Pinterest visual search and object detection infrastructure, deep-learning visual embeddings and classification, camera-based mobile capture (iOS/Android), recommendation systems serving 10B daily recommendations, human curation pipeline for shoppable results.

## Results
- Visual search served hundreds of millions of searches per month with billions of objects detected — one of Pinterest's most-used features.
- Lens (beta), Shop the Look, and Instant Ideas rolled out across iOS, Android, and web as launch-stage products; no per-product engagement metrics are reported in the post.

## Takeaways
- A single visual understanding platform can amortize across many products: camera search, shopping, and feed personalization all consumed the same infrastructure.
- The frontier moved from "find visually similar images" to "understand the object and its use" — similarity is table stakes, intent is the differentiator.
- Hybrid ML-plus-curation is a pragmatic recipe when results must be commercially trustworthy.
