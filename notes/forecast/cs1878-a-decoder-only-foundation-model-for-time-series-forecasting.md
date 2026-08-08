---
id: cs1878
title: A decoder-only foundation model for time-series forecasting (TimesFM)
company: Google
primary_category: forecast
sub_category: time-series
year: 2024
source_url: https://research.google/blog/a-decoder-only-foundation-model-for-time-series-forecasting/
tags: [foundation-model, time-series, patch-tokenization, decoder-only, zero-shot-forecasting]
---

# A decoder-only foundation model for time-series forecasting (TimesFM)
**Google** · 2024 · [source](https://research.google/blog/a-decoder-only-foundation-model-for-time-series-forecasting/)

## Problem
Supervised time series models must be retrained for each new domain and forecast horizon, creating substantial operational burden at scale. Google Research sought a single pretrained model capable of zero-shot forecasting across varied domains without task-specific fine-tuning.

## Approach / System design
TimesFM is a 200-million-parameter decoder-only transformer that treats time series forecasting analogously to next-token prediction in language models. Input time series are divided into fixed-length patches, and the model is trained to predict longer output patches in a single forward pass, allowing variable forecast horizons without retraining. Pretraining used 100 billion time-points drawn from diverse real and synthetic sources.

## Key decisions
Adopting a decoder-only architecture mirrors the design philosophy of large language models, enabling autoregressive generation of forecast horizons of varying length. Patch-based input tokenization reduces the sequence length the transformer must attend over while preserving local temporal structure. Longer output patches at inference time avoid the compounding errors of step-by-step autoregressive decoding.

## Stack
Decoder-only transformer, patch-based tokenization, pretrained on 100B time-points, deployed as BigQuery ML AI.FORECAST.

## Results
TimesFM demonstrates competitive zero-shot forecasting performance across standard benchmarks and has been integrated into BigQuery ML as the AI.FORECAST capability, making it available at Google Cloud scale.

## Takeaways
Decoder-only transformer architectures trained on large diverse corpora transfer well to zero-shot time series forecasting, mirroring the success seen in natural language. Patch tokenization is a key design choice that makes attending over long time series tractable while preserving local temporal patterns.
