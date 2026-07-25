---
id: cs2326
title: Bringing Locations to Life with AR: Snapchat Landmarkers
company: Snap
primary_category: cv
sub_category: segmentation
year: 2020
source_url: https://eng.snap.com/life-with-ar-landmarkers
tags: [ar, segmentation, 3d-reconstruction, slam, location, scene-understanding]
---

# Bringing Locations to Life with AR: Snapchat Landmarkers
**Snap** · 2020 · [source](https://eng.snap.com/life-with-ar-landmarkers)

## Problem
Snapchat's Landmarkers — AR experiences anchored to real-world places — existed only for roughly 30 iconic locations (e.g., the Gateway of India, the Great Sphinx), because each template required collecting large amounts of imagery of the location, which took significant time and resources. The AR creator community wanted to anchor Lenses to thousands of local places, so Snap needed a scalable, self-serve way for creators to make their own location anchors.

## Approach / System design
Custom Landmarkers use a two-tier 3D representation of a place:
- **Tracking model**: a custom SLAM-based system building on natural feature tracking (leveraging ARKit/ARCore foundations) that detects and tracks visual features of the location with high accuracy when a user unlocks the experience, keeping AR content locked to the real structure.
- **Creator mesh**: a LiDAR-captured 3D mesh of the location that lens creators build against. LiDAR sensors emit invisible light and infer structure from the light's return time, giving a usable 3D scan without a photogrammetry pipeline.
Creator workflow: scan the location with the "Custom Landmarker Creator" Lens on a LiDAR-enabled phone (iPhone 12 Pro and later); the system generates a unique ID and 3D mesh; the creator imports that ID into Lens Studio and builds the AR experience against the mesh.

## Key decisions
- LiDAR scanning over photogrammetry as the primary capture path once LiDAR phones became available — simpler for creators — with photogrammetry supported as an optional supplement.
- Separate representations for tracking (feature-based SLAM model) and authoring (mesh), each optimized for its consumer.
- UX-first scanning flow: multiple rounds of user testing led to visual and animation guidance replacing text instructions, and "Perspective Capture" 3D visualizations to clarify the second scanning phase.
- Democratize creation through self-serve tooling rather than scaling Snap's internal template production.

## Stack
ARKit and ARCore (SLAM foundations), custom natural-feature-tracking pipeline, LiDAR capture (iPhone 12 Pro+), Custom Landmarker Creator Lens, Lens Studio authoring platform.

## Results
No quantitative metrics are disclosed in the article. The system moved location-anchored AR from ~30 company-built landmark templates to a creator-driven model where any suitable local place can be scanned and authored against.

## Takeaways
- Scaling location AR meant converting an internal content-production pipeline into a creator tool — the bottleneck was capture cost, not rendering.
- Emerging commodity hardware (phone LiDAR) can replace an expensive reconstruction pipeline at acceptable quality.
- For consumer-facing 3D capture, scanning UX (animations, visual guidance) is as critical as the underlying computer vision.
