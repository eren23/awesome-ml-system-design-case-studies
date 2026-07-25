---
id: cs2192
title: Building a Large Geospatial Model to Achieve Spatial Intelligence
company: Niantic
primary_category: cv
sub_category: embeddings
year: 2024
source_url: https://nianticlabs.com/news/largegeospatialmodel
tags: [geospatial, neural-implicit-representation, visual-positioning, visual-localization, large-scale, neural-radiance-fields, ar, vps]
---

# Building a Large Geospatial Model to Achieve Spatial Intelligence
**Niantic** · 2024 · [source](https://nianticlabs.com/news/largegeospatialmodel)

## Problem
Machines lack the spatial understanding humans take for granted — imagining a familiar structure from an unseen angle or inferring the parts of a scene they haven't observed. Existing AI models can't extrapolate places from novel viewpoints, which limits AR, robotics, and autonomous systems. Niantic's location-specific neural maps each work in isolation, so knowledge learned at one place can't help understand another.

## Approach / System design
Niantic proposes a Large Geospatial Model (LGM): a global model that distills the common information across millions of independently trained local neural networks, enabling knowledge sharing between them. Today its Visual Positioning System (VPS) is powered by over 50 million local neural networks totaling more than 150 trillion parameters, each implicitly encoding a physical location in its weights (built on the ACE 2023 and ACE Zero 2024 line of work, combining classical structure-from-motion with implicit neural representations). The system draws on 10 million scanned locations worldwide, of which about 1 million are activated for VPS, and receives roughly 1 million fresh scans per week, each containing hundreds of discrete images. The LGM consolidates these local models so that observations of one location inform predictions about partially observed ones; MicKey (2024) serves as a proof of concept for relative pose estimation under drastic viewpoint changes.

## Key decisions
- Move from isolated per-location neural maps to a global model that transfers knowledge across locations, analogous to how LLMs generalize across text.
- Keep representations metric-bound — precise estimates in scale-metric units — rather than the unscaled geometry of generic 3D models, so positioning stays centimeter-accurate.
- Build on pedestrian-perspective scan data collected through Niantic's games, giving ground-level coverage that satellite or street-vehicle imagery misses.
- Use large-scale weekly scan ingestion to keep local models fresh and continuously expand coverage.

## Stack
Local implicit neural networks per location (ACE / ACE Zero lineage), structure-from-motion classical 3D vision, MicKey for cross-viewpoint pose estimation, VPS serving infrastructure over ~1M activated locations.

## Results
- 50M+ trained neural networks, 150T+ combined parameters backing the production VPS.
- 10 million scanned locations, ~1 million live for VPS, ~1 million new scans ingested weekly.
- Centimeter-level positioning accuracy for AR applications; the unified LGM itself is presented as the forward-looking research direction rather than a shipped result.

## Takeaways
Scaling spatial intelligence looks like scaling language models: many local specialists can be distilled into a shared global prior that extrapolates to under-observed places. Metric grounding is what separates a usable geospatial model from generic 3D generation. Applications reach beyond gaming into logistics, robotics, spatial planning, and remote collaboration.
