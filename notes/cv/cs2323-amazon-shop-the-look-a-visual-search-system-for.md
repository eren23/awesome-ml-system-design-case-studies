---
id: cs2323
title: Amazon Shop the Look: A Visual Search System for Fashion and Home
company: Amazon
primary_category: cv
sub_category: object-detection
year: 2022
source_url: https://www.amazon.science/publications/amazon-shop-the-look-a-visual-search-system-for-fashion-and-home
tags: [visual-search, fashion, ecommerce, deep-learning, object-detection, retrieval]
---

# Amazon Shop the Look: A Visual Search System for Fashion and Home
**Amazon** · 2022 · [source](https://www.amazon.science/publications/amazon-shop-the-look-a-visual-search-system-for-fashion-and-home)

## Problem
Customers want to find fashion and home products by photographing or uploading an image rather than typing text. Building this at Amazon scale means bridging the domain gap between in-the-wild query photos and studio-style catalog imagery, indexing a dynamic catalog of billions of products, and serving retrieval at low latency.

## Approach / System design
Shop the Look is a web-scale production visual search system composed of:
- **Vision models**: object detection, recognition, and feature-extraction (embedding) models trained on large-scale image data from the Amazon product catalog.
- **Index-building pipeline**: an offline pipeline that builds and refreshes the retrieval index over the billions-of-products catalog as it changes.
- **Runtime service**: a low-latency online service that detects products in the query image, extracts embeddings, and retrieves visually similar catalog items.
The paper also describes strategies to reduce the human annotation effort required to train these models at catalog scale, and reports both quantitative and qualitative evaluations of the deployed system.

## Key decisions
- Explicitly address the query/catalog domain gap (real-world photos vs. controlled product photography) in model design rather than assuming matched distributions.
- Design the indexing pipeline for a continuously changing catalog instead of a static corpus.
- Trade off model accuracy against serving efficiency to keep user-facing latency low.
- Lean on the catalog itself as large-scale training data, with annotation-efficiency strategies instead of full manual labeling.

## Stack
Deep-learning-based detection, recognition, and embedding models; large-scale offline indexing infrastructure; low-latency online retrieval service. Specific frameworks and index technologies are not named in the source.

## Results
The publication reports quantitative and qualitative evaluation results for the deployed system and states that the fast-growing Shop the Look service is shaping how customers shop on Amazon; specific metric values are not given in the abstract.

## Takeaways
- Production visual search is as much an indexing-and-serving problem as a modeling problem: the offline pipeline and runtime service carry equal weight to the models.
- Domain adaptation between user photos and catalog imagery is the central modeling challenge for e-commerce visual search.
- Annotation-efficiency strategies are necessary to make training tractable against a billions-scale, ever-changing catalog.
