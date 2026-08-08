---
id: cs1877
title: Chronos: Adapting language model architectures for time series forecasting
company: Amazon
primary_category: forecast
sub_category: time-series
year: 2024
source_url: https://www.amazon.science/blog/adapting-language-model-architectures-for-time-series-forecasting
tags: [foundation-model, time-series, tokenization, transformer, zero-shot-forecasting]
---

# Chronos: Adapting language model architectures for time series forecasting
**Amazon** · 2024 · [source](https://www.amazon.science/blog/adapting-language-model-architectures-for-time-series-forecasting)

## Problem
Most time series forecasting models are dataset-specific and require retraining for each new domain, creating high operational overhead at scale. Amazon sought a foundation model capable of zero-shot forecasting across diverse time series without domain-specific fine-tuning.

## Approach / System design
Chronos converts continuous time series into discrete tokens by first scaling each series and then applying uniform quantization, allowing off-the-shelf language model transformer architectures to be trained directly on the tokenized sequences. Training data is augmented with TSMix (a mixing-based augmentation technique) and KernelSynth (a synthetic data generator) to broaden the distribution of seen patterns.

## Key decisions
Reusing existing transformer language model architectures without fundamental changes was a deliberate choice, enabling the team to leverage mature infrastructure and training recipes from the NLP domain. Scaling and quantization as the tokenization strategy bridges the gap between continuous numerical data and the discrete token vocabulary that LMs require.

## Stack
Transformer-based language model architecture, scaling and quantization tokenization, TSMix data augmentation, KernelSynth synthetic data generation.

## Results
Not covered in the source.

## Takeaways
Adapting language model architectures for time series by treating scaled-and-quantized values as tokens is a viable route to a general-purpose zero-shot forecasting foundation model. Synthetic data generation and augmentation strategies are important complements to real-world training corpora for broadening generalization.
