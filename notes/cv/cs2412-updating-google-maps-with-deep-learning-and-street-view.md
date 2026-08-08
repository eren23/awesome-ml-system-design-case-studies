---
id: cs2412
title: "Updating Google Maps with Deep Learning and Street View"
company: Google
primary_category: cv
sub_category: object-detection
year: 2021
source_url: https://research.google/blog/updating-google-maps-with-deep-learning-and-street-view/
tags: [street-view, google-maps, text-recognition, ocr, deep-learning, object-detection, production, maps]
---

# Updating Google Maps with Deep Learning and Street View
**Google** · 2021 · [source](https://research.google/blog/updating-google-maps-with-deep-learning-and-street-view/)

## Problem
Keeping Google Maps accurate at a global scale is impossible through manual curation alone. Addresses, business names, road signs, and other map features change constantly, and the sheer volume of Street View imagery collected worldwide requires automated methods to detect and extract this information reliably.

## Approach / System design
Google applies deep learning models to Street View imagery to automatically detect and recognize text and objects of map-relevance, including building addresses, business names, and road features. The pipeline processes raw Street View frames, localizes regions of interest using object detection, and then applies OCR and classification models to extract structured data that can be fed into the Maps database. Results from multiple image frames are aggregated to improve confidence before updating the map.

## Key decisions
Not covered in the source.

## Stack
Deep learning models for object detection and OCR applied to Street View imagery; the broader Google Maps data infrastructure handles downstream ingestion and validation.

## Results
Not covered in the source.

## Takeaways
Combining object detection with optical character recognition in a Street View pipeline enables Maps data to be refreshed at a scale and cadence that manual approaches cannot match. Aggregating evidence from multiple frames of the same location before committing an update is a key quality control mechanism that reduces errors caused by occlusion or image artifacts.
