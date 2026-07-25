---
id: cs2166
title: Training Large-Scale Recommendation Models with TPUs
company: Snap
primary_category: ads
sub_category: ctr-prediction
year: 2022
source_url: https://cloud.google.com/blog/products/ai-machine-learning/snap-inc-uses-google-cloud-tpu-for-deep-learning-recommendation-models/
tags: [tpu, deep-learning-recommendation-model, large-scale-training, cost-optimization, throughput, training infrastructure, recommendation system, deep learning, ad ranking, google cloud, distributed training]
---

# Training Large-Scale Recommendation Models with TPUs
**Snap** · 2022 · [source](https://cloud.google.com/blog/products/ai-machine-learning/snap-inc-uses-google-cloud-tpu-for-deep-learning-recommendation-models/)

## Problem
Snap trains deep learning ad-ranking models for 300+ million daily users and millions of ads. The ML workflow is iterative — train, evaluate, retrain — so experiment cycles measured in days (or weeks) on CPU/GPU infrastructure directly limited how many model ideas the team could try and how good the shipped ranking models could be.

## Approach / System design
Snap benchmarked Google Cloud TPUs against its existing CPU- and GPU-based training and migrated production ad-ranking model training to TPUs. Recommendation models are dominated by large embedding lookups, so Snap leaned on the TPU Embedding API as the native path for embedding operations, exploiting the TPUs' fast lookups and high memory bandwidth. Models train iteratively on user–ad interaction logs.

## Key decisions
- Choose purpose-built ML ASICs (TPUs) over general-purpose CPUs and GPUs after direct benchmarking of throughput and cost.
- Use the TPU Embedding API rather than hand-rolled embedding handling, matching the models' embedding-heavy profile to the hardware's strengths.
- Optimize for experiment velocity: prefer hours-long training cycles to enable many more iterations.

## Stack
Google Cloud TPUs, TPU Embedding API, deep learning recommendation models for ad ranking; prior infrastructure was CPU- then GPU-based.

## Results
- 74% cost reduction and 250% throughput increase vs. CPU training for a standard ad recommendation model.
- GPUs measured 67% worse throughput and 52% higher cost than TPUs on Snap's workload.
- Training time went from weeks to hours.

## Takeaways
For embedding-heavy recommendation workloads, hardware fit matters enormously — an accelerator with native embedding support beat both CPUs and GPUs on cost and speed. The deeper win is velocity: faster training means more experiments, and at Snap's scale even a 1% model improvement carries significant monetary impact.
