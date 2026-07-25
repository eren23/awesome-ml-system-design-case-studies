---
id: cs2329
title: Introducing a New Way to Visually Search on Pinterest
company: Pinterest
primary_category: cv
sub_category: visual-search
year: 2020
source_url: https://medium.com/pinterest-engineering/introducing-a-new-way-to-visually-search-on-pinterest-67c8284b3684
tags: [visual-search, lens, mobile, object-detection, embeddings, camera]
---

# Introducing a New Way to Visually Search on Pinterest
**Pinterest** · 2020 · [source](https://medium.com/pinterest-engineering/introducing-a-new-way-to-visually-search-on-pinterest-67c8284b3684)

## Problem
Pinterest's discovery products (Guided Search, Related Pins) were built on textual descriptions and Pin-to-board connections, but the richest signal in every Pin — the image itself — was unused. A Pin's image contains dozens of interesting objects, and users had no way to search for a specific item (say, a lamp inside a living-room photo) without the right words to describe it.

## Approach / System design
- **Deep-learned image features**: in collaboration with the Berkeley Vision and Learning Center, the team used deep learning to learn image representations from Pinterest's richly annotated dataset of billions of Pinner-curated Pins. These features yield a similarity score between any two images.
- **Distributed index and search**: to compare a query feature against billions of others, they built a distributed index and search system from open-source tools that scales to billions of images and returns thousands of visually similar results in a fraction of a second.
- **Crop-to-search UX**: users tap the search tool on a Pin, drag a zoom/crop box over the object of interest, and get visually similar Pins in real time for that region.
- **Beyond duplicates**: ranking optimizes visual similarity rather than duplicate detection, surfacing exact matches alongside items similar in style, pattern, or shape.
- The same visual signals were also being tested to improve Related Pins, detailed in an accompanying white paper (with a KDD'15 paper covering earlier work).

## Key decisions
- Learn features from Pinterest's own billions of annotated Pins rather than generic datasets, exploiting Pinner curation as free supervision.
- Build the retrieval layer on open-source tooling as a distributed index instead of a bespoke system.
- Let users specify the query region via cropping instead of only whole-image search, since Pins contain many objects.
- Optimize for stylistic similarity, not just exact matches, to serve discovery rather than lookup.
- Ship fast: the core system was built by a team of four engineers in a few months.

## Stack
Deep learning feature extraction (Berkeley collaboration, Caffe team acknowledged), distributed similarity index built on open-source tools, real-time retrieval over billions of images, crop-tool UI on iOS, Android, and web.

## Results
- Sub-second retrieval of thousands of visually similar results from an index of billions of images.
- Rolled out globally to all platforms (iOS, Android, web).
- Visual signals were concurrently shown to improve Related Pins in experiments (detailed in the released white paper); no specific engagement numbers appear in the post.

## Takeaways
- A platform's own user-curated content can serve as a massive labeled dataset for representation learning.
- Region-based (crop) querying turns one image into many possible queries and matches how users actually think about objects in scenes.
- A small team can ship web-scale visual search quickly by combining learned embeddings with open-source distributed indexing.
- The system was designed to improve with usage: more Pinning means better features and results.
