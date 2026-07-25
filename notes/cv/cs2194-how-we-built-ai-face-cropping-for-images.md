---
id: cs2194
title: How we built AI face cropping for Images
company: Cloudflare
primary_category: cv
sub_category: image-classification
year: 2025
source_url: https://blog.cloudflare.com/ai-face-cropping-for-images/
tags: [face-detection, RetinaFace, image-cropping, cnn, workers-ai, gpu, smart-crop, edge-inference]
---

# How we built AI face cropping for Images
**Cloudflare** · 2025 · [source](https://blog.cloudflare.com/ai-face-cropping-for-images/)

## Problem
Cloudflare Images needed automatic face-aware cropping (profile pictures, e-commerce thumbnails) at edge scale. The beta ran CPU inference inside the Images service via TensorFlow Rust, which leaked memory and spiked global RAM consumption enough to trigger service alerts, threatening stability as traffic grew.

## Approach / System design
A RetinaFace convolutional neural network detects faces; the crop is computed from an outer bounding box around all detected faces, using its center as the focal point. Input images are downscaled to at most 1024×1024 (preserving aspect ratio) before inference. After the CPU prototype's memory problems — partially mitigated by swapping glibc malloc for jemalloc — the workload was moved off the Images service entirely onto GPU inference in Workers AI, isolating face detection from the rest of the Images pipeline.

## Key decisions
- Chose RetinaFace over BlazeFace, R-CNN, and YOLO for the best precision (99.4% cited) with one-stage detector speed.
- Capped inference resolution at 1024×1024 to bound compute.
- Encompass all faces with an outer bounding box rather than centering on the single largest face, giving more balanced crops for group shots.
- Migrated from in-service CPU inference to isolated GPU serving on Workers AI to solve memory contention structurally.
- Privacy-first scope: detection only — no facial recognition or identification.

## Stack
RetinaFace CNN; initially TensorFlow Rust on CPU (glibc malloc → jemalloc); production on Workers AI GPU container framework, integrated with Cloudflare Images transformations.

## Results
Switching to jemalloc saved roughly 20 TiB of memory globally; after the GPU migration each Images instance consumes about 150 MiB. A reference customer serves 45 million unique transformations per month using the feature.

## Takeaways
Running ML inference inside a latency-critical service on CPU is a stability trap; moving models to a shared GPU serving platform (Workers AI) fixed memory safety and scalability at once. Allocator choice alone was worth terabytes of fleet memory, but isolation was the durable fix.
