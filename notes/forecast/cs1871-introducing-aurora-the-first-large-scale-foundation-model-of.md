---
id: cs1871
title: Introducing Aurora: The first large-scale foundation model of the atmosphere
company: Microsoft
primary_category: forecast
sub_category: time-series
year: 2024
source_url: https://www.microsoft.com/en-us/research/blog/introducing-aurora-the-first-large-scale-foundation-model-of-the-atmosphere/
tags: [foundation-model, weather-forecasting, swin-transformer, azure-ai-foundry, air-pollution]
---

# Introducing Aurora: The first large-scale foundation model of the atmosphere
**Microsoft** · 2024 · [source](https://www.microsoft.com/en-us/research/blog/introducing-aurora-the-first-large-scale-foundation-model-of-the-atmosphere/)

## Problem
Existing AI weather models are typically trained on a single data source and target a single task, limiting their ability to generalize across resolutions, variable sets, and forecast types. Extreme weather events such as rapid-intensification storms exposed accuracy gaps in both traditional NWP and first-generation AI models, motivating a more general foundation model approach.

## Approach / System design
Aurora is a 1.3 billion-parameter foundation model built on a flexible 3D Swin Transformer backbone with Perceiver-based encoders and decoders that can ingest heterogeneous inputs at different resolutions and pressure levels. Pretraining spans more than a million hours of diverse atmospheric data including ERA5 reanalysis, CMIP6 climate simulations, operational IFS and GFS forecasts, and CAMS atmospheric chemistry data. Fine-tuning proceeds in two stages: a short-lead-time phase that refines pretrained weights, followed by a long-lead-time rollout phase using Low Rank Adaptation (LoRA) to efficiently adapt the model without full retraining.

## Key decisions
Training on multiple heterogeneous datasets was shown to significantly outperform single-dataset training, making diverse pretraining a first-order design principle rather than an afterthought. LoRA fine-tuning for long-lead-time rollout keeps the parameter count manageable while adapting the model to the specific error dynamics of extended autoregressive forecasting. The Perceiver-based encoder/decoder design accommodates varying input/output specifications without requiring a fixed grid or variable set.

## Stack
3D Swin Transformer backbone, Perceiver-based encoders and decoders, LoRA fine-tuning, pretraining data from ERA5, CMIP6, IFS, GFS, and CAMS, deployed via Azure AI Foundry.

## Results
Aurora achieves an estimated 5,000x speedup over the IFS and operates at 0.1-degree spatial resolution. It outperforms GraphCast on 94% of forecast targets, with 40% improvement in upper-atmosphere predictions and 10-15% gains at short and long lead times. On air pollution forecasting, Aurora matches or outperforms operational CAMS on 74% of targets. It demonstrated superior performance on extreme weather prediction compared to both GraphCast and IFS-HRES.

## Takeaways
Diverse pretraining across heterogeneous atmospheric datasets is the single most impactful factor in Aurora's generalization capability. A foundation model paradigm — pretraining once on broad data and fine-tuning for specific tasks — applies to atmospheric science as effectively as it has in NLP and computer vision. The ability to handle air quality and greenhouse gas prediction alongside weather forecasting in a single model demonstrates the breadth that scale and diverse pretraining enable.
