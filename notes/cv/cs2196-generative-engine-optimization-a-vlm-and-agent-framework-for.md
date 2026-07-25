---
id: cs2196
title: "Generative Engine Optimization: A VLM and Agent Framework for Pinterest Acquisition Growth"
company: Pinterest
primary_category: cv
sub_category: vlm
year: 2026
source_url: https://arxiv.org/abs/2602.02961
tags: [vlm, visual-search, reverse-search-design, SigLIP, HNSW, ANN, two-tower, seo, discovery, fine-tuning]
---

# Generative Engine Optimization: A VLM and Agent Framework for Pinterest Acquisition Growth
**Pinterest** · 2026 · [source](https://arxiv.org/abs/2602.02961)

## Problem
Generative search systems (ChatGPT, Gemini, Claude) answer users directly on-page instead of sending them to websites, threatening to disintermediate visual platforms. Individual images lack the semantic depth and authority signals that generative engines prioritize when choosing what to cite, so Pinterest's billions of visual assets risked becoming invisible to the new discovery channel.

## Approach / System design
Pinterest built a production-scale Generative Engine Optimization (GEO) framework. Fine-tuned vision-language models perform "reverse search design": instead of captioning an image, they predict the actual search queries users would type to find it. AI agents mine real-time internet trends to surface emerging search demand. These signals drive construction of semantically coherent Collection Pages — aggregations of related images built via multimodal embeddings — that carry the topical depth and authority generative engines reward. A hybrid VLM plus two-tower ANN architecture creates authority-aware interlinking across the billion-scale image corpus, optimizing the embedding space for generative retrieval.

## Key decisions
- Reverse search design over conventional captioning: model outputs are query-shaped, aligning content representation with how demand is actually expressed.
- Aggregate images into Collection Pages rather than optimizing single pins, since pages with semantic coherence earn authority in generative retrieval.
- Combine expressive VLM inference with scalable two-tower ANN retrieval so the system works over billions of images and tens of millions of collections.
- Use trend-mining agents to target emerging queries rather than only historical demand.

## Stack
Fine-tuned vision-language models, agentic trend-mining pipeline, multimodal embeddings, two-tower ANN retrieval architecture, deployed over billions of images and tens of millions of Collection Pages.

## Results
- 20% organic traffic growth in production, contributing to multi-million monthly-active-user growth.
- Framework deployed at full corpus scale (billions of images, tens of millions of collections).

## Takeaways
Visual platforms can stay discoverable in the generative-search era by reshaping content into query-aligned, semantically coherent aggregations rather than relying on individual assets. Predicting user queries from content inverts the classic captioning framing and directly optimizes for how generative engines retrieve and cite. Hybrid VLM + ANN architectures make this tractable at billion-item scale.
