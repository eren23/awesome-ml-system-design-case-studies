---
id: cs1875
title: Pangu-Weather: AI model outperforms NWP for medium-range forecasting
company: Huawei Cloud
primary_category: forecast
sub_category: time-series
year: 2023
source_url: https://www.huaweicloud.com/intl/en-us/about/blogs/20230707.html
tags: [weather-forecasting, 3D-transformer, earth-specific-bias, hierarchical-temporal-aggregation, ECMWF]
---

# Pangu-Weather: AI model outperforms NWP for medium-range forecasting
**Huawei Cloud** · 2023 · [source](https://www.huaweicloud.com/intl/en-us/about/blogs/20230707.html)

## Problem
Medium-range weather forecasting at global scale has historically been dominated by physics-based NWP systems such as ECMWF's IFS, which require large supercomputing clusters and hours of wall-clock time per forecast cycle. The challenge was building an AI model that could match or exceed IFS accuracy while reducing inference time by orders of magnitude.

## Approach / System design
Pangu-Weather uses a 3D Earth-Specific Transformer that treats the atmosphere as a three-dimensional grid, incorporating earth-specific positional biases to encode the physical structure of the atmosphere. Hierarchical temporal aggregation trains separate model weights for 1-hour, 3-hour, 6-hour, and 24-hour steps, enabling efficient multi-step inference by selecting the optimal combination of step sizes to reach the target lead time while minimising error accumulation.

## Key decisions
Designing earth-specific positional biases within the transformer acknowledges that atmospheric dynamics differ substantially by altitude and latitude, properties that generic positional encodings do not capture. Hierarchical temporal aggregation trades the computational overhead of training multiple models for reduced iterative error accumulation at long lead times.

## Stack
3D Earth-Specific Transformer, hierarchical temporal aggregation (1h/3h/6h/24h model weights), trained on ERA5 reanalysis, results viewable live on ECMWF's website.

## Results
Pangu-Weather produces a medium-range global forecast in approximately 1.4 seconds per run and outperforms ECMWF's IFS on standard medium-range forecast metrics. ECMWF hosts live Pangu-Weather forecast output on its website.

## Takeaways
Incorporating physically motivated priors such as earth-specific positional encodings into transformer architectures improves weather forecasting accuracy. Hierarchical temporal aggregation is an effective strategy for controlling error accumulation in autoregressive forecast models without sacrificing long-range forecast skill.
