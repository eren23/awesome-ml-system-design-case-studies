---
id: cs1843
title: Chaining iOS Machine Learning, Computer Vision, and Augmented Reality to Make the Magical Real
company: Etsy
primary_category: cv
sub_category: object-detection
year: 2020
source_url: https://www.etsy.com/codeascraft/chaining-ios-machine-learning-computer-vision-and-augmented-reality-to-make-the-magical-real/
tags: [augmented-reality, apple-vision-framework, core-image, rectangle-detection, wall-art]
---

# Chaining iOS Machine Learning, Computer Vision, and Augmented Reality to Make the Magical Real
**Etsy** · 2020 · [source](https://www.etsy.com/codeascraft/chaining-ios-machine-learning-computer-vision-and-augmented-reality-to-make-the-magical-real/)

## Problem
Etsy sellers list wall art in images showing frames at various angles, making it difficult for buyers to visualize how a piece would actually look on their own walls. A feature to preview artwork in the buyer's physical space needed to handle imperfect listing photos, correct for perspective distortion, and place the artwork at true-to-scale dimensions in augmented reality.

## Approach / System design
The feature chains three Apple frameworks in sequence. The Vision framework's rectangle detection identifies the artwork boundary in the listing photo. Core Image performs a perspective-corrected crop on the detected rectangle, producing a front-on, undistorted version of the artwork. ARKit then places the corrected artwork image onto the user's detected wall surface, scaled to real-world dimensions so the piece appears at its actual size in the scene.

## Key decisions
Using Apple's on-device frameworks (Vision, Core Image, ARKit) avoids server round-trips and keeps the feature entirely local, which is important for responsiveness and privacy. Chaining the three steps sequentially — detect, correct, place — decomposes a complex AR task into well-defined sub-problems each solved by a specialized API. Perspective correction is a necessary intermediate step; skipping it would result in distorted artwork in the AR view.

## Stack
Apple Vision framework (rectangle detection), Core Image (perspective-corrected cropping), ARKit (augmented reality placement and wall detection), iOS.

## Results
Not covered in the source.

## Takeaways
Chaining multiple on-device computer vision and AR frameworks enables sophisticated user experiences without backend infrastructure. Perspective correction is often an overlooked but essential preprocessing step when working with real-world object images captured at arbitrary angles.
