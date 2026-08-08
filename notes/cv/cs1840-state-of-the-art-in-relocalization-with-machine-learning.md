---
id: cs1840
title: State of the ARt in Relocalization with Machine Learning (ACE)
company: Niantic
primary_category: cv
sub_category: embeddings
year: 2023
source_url: https://web.archive.org/web/20251018174054/https://nianticlabs.com/news/research-ace
tags: [relocalization, visual-positioning-system, scene-coordinate-regression, neural-mapping, ar]
---

# State of the ARt in Relocalization with Machine Learning (ACE)
**Niantic** · 2023 · [source](https://web.archive.org/web/20251018174054/https://nianticlabs.com/news/research-ace)

## Problem
Camera relocalization — determining where a device camera is positioned within a known environment — is a core requirement for AR experiences. Traditional approaches rely on large 3D point-cloud maps that consume significant storage and are slow to build, making them impractical at a scale of hundreds of thousands of real-world locations.

## Approach / System design
Niantic's ACE (Accelerated Coordinate Encoding) replaces the conventional 3D point-cloud map with a compact neural network that learns a mapping from image patches to scene coordinates. A single ACE network encodes all the spatial information needed for relocalization into roughly 4 MB of model weights, trained per location. At inference time, the model predicts scene coordinates from query image features, which are then used to solve for the camera pose via a RANSAC-based estimator.

## Key decisions
Compressing the map representation into a neural network rather than a sparse point cloud was the central architectural choice, dramatically shrinking storage per location. Training was designed to complete in approximately 5 minutes per location, enabling rapid map creation at scale. The system was integrated into Lightship VPS so that existing Niantic infrastructure could benefit without major re-engineering.

## Stack
Scene-coordinate regression network (ACE), neural mapping, visual positioning system (Lightship VPS), RANSAC-based pose estimation. Compared against the DSAC* baseline.

## Results
ACE trains maps roughly 300 times faster than the DSAC* baseline while maintaining competitive relocalization accuracy. The system powers the majority of Lightship VPS relocalizations across approximately 200,000 locations.

## Takeaways
Encoding scene geometry into neural network weights rather than explicit point clouds achieves a far better trade-off between map size, build time, and relocalization quality. The approach demonstrates that learned representations can replace hand-crafted 3D structures in large-scale deployed AR systems.
