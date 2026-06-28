---
id: cs0798
title: "Enhancing Brand Visibility and Trust with On device ML models: A Journey at Swiggy"
company: Swiggy
primary_category: cv
sub_category: object-detection
year: 2025
source_url: https://bytes.swiggy.com/enhancing-brand-visibility-and-trust-with-on-device-ml-models-a-journey-at-swiggy-e3e626f96c52
tags: [CV]
---

# Enhancing Brand Visibility and Trust with On device ML models: A Journey at Swiggy
**Swiggy** · 2025 · [source](https://bytes.swiggy.com/enhancing-brand-visibility-and-trust-with-on-device-ml-models-a-journey-at-swiggy-e3e626f96c52)

## Problem
Swiggy wanted delivery executives (DEs) to wear Swiggy-branded gear (t-shirts, jackets, bags) for brand visibility and trust, and needed to automatically verify compliance from photos in real time. The key constraint: minimize false negatives (missing gear that is actually present). DEs often work in areas with poor connectivity, so detection must be fast and not depend on the network.

## Approach / System design
Run image classification on-device rather than server-side. A first attempt at simple color detection failed due to color variation across gear versions and obstructions (helmets/jackets). They pivoted to a lightweight on-device CNN: a MobileNet image classifier trained with TensorFlow Lite Model Maker, quantized, and embedded in the React Native app via Vision Camera's custom frame processor to classify live camera frames.

## Key decisions
- On-device over server-side to avoid latency and connectivity dependence in time-sensitive delivery flows.
- MobileNet base for efficiency on low-end devices; post-training quantization (TFLite Optimize.DEFAULT) to shrink the model.
- Selective frame processing (sample a small fraction of frames) and battery/memory health checks that pause inference under low-resource conditions.
- Phased rollout: a few cities first to measure cross-device latency, then nationwide.

## Stack
TensorFlow Lite + TFLite Model Maker; MobileNet; Google Colab for training; React Native app with Vision Camera frame processor. Dataset: ~20,000 gear-present and ~3,000 gear-absent photos, resized to 224x224, 90/10 train/test split.

## Results
- 90%+ classification accuracy; quantized model only ~3.4MB.
- ~150ms inference latency (p95) on low-end Android.
- <0.25% of daily battery usage; zero additional app crashes.
- 95%+ of DEs now use the latest gear; 6M+ monthly on-device inferences.
- Extended the on-device approach to blur and darkness detection for image quality.

## Takeaways
For real-time, connectivity-independent verification, a small quantized MobileNet on-device beats a server API on latency and reliability. The hard part is not training accuracy but production hygiene: selective frame sampling and resource-aware pausing keep battery/crash impact negligible at millions of inferences.
