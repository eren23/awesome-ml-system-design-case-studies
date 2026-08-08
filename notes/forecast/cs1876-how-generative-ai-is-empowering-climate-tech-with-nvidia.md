---
id: cs1876
title: How generative AI is empowering climate tech with NVIDIA Earth-2
company: NVIDIA
primary_category: forecast
sub_category: time-series
year: 2024
source_url: https://developer.nvidia.com/blog/how-generative-ai-is-empowering-climate-tech-with-nvidia-earth-2/
tags: [earth-2, CorrDiff, diffusion-downscaling, FourCastNet, typhoon-forecasting]
---

# How generative AI is empowering climate tech with NVIDIA Earth-2
**NVIDIA** · 2024 · [source](https://developer.nvidia.com/blog/how-generative-ai-is-empowering-climate-tech-with-nvidia-earth-2/)

## Problem
Global weather model output is typically available at coarse resolutions of around 25 km, insufficient for local impact forecasting such as urban flooding or typhoon track and intensity at landfall. Statistical downscaling techniques have historically introduced blurring artifacts and failed to reconstruct fine-scale extremes accurately.

## Approach / System design
NVIDIA's Earth-2 platform combines FourCastNet as a fast global forecast backbone with CorrDiff, a two-step diffusion-based downscaling model. CorrDiff first produces a regression correction to the global model output and then applies a diffusion model conditioned on the corrected field to generate high-resolution fine-scale detail. By running CorrDiff multiple times, the platform produces ensemble uncertainty estimates at the 2 km output resolution alongside the deterministic downscaled forecast.

## Key decisions
The two-step correction-then-diffusion design in CorrDiff separates large-scale bias correction from fine-scale detail synthesis, allowing each stage to be trained and evaluated independently. Pairing a fast physics-informed backbone (FourCastNet) with a learned downscaling model retains the global dynamical consistency of the backbone while adding regional fine-scale accuracy.

## Stack
FourCastNet (global forecast backbone), CorrDiff (two-step diffusion downscaling model), ensemble uncertainty via stochastic sampling, deployed by Taiwan's Central Weather Administration (CWA) for typhoon forecasting.

## Results
Earth-2 with CorrDiff downscales global weather from 25 km to 2 km resolution. The system has been deployed operationally by Taiwan's Central Weather Administration for typhoon forecasting with ensemble uncertainty quantification.

## Takeaways
Combining a fast global backbone model with a generative diffusion downscaling model is an effective architecture for regional high-resolution forecasting. Diffusion-based downscaling preserves fine-scale extreme statistics better than classical statistical methods while enabling ensemble uncertainty quantification through stochastic sampling.
