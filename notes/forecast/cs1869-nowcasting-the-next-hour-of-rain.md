---
id: cs1869
title: Nowcasting the next hour of rain
company: Google DeepMind
primary_category: forecast
sub_category: time-series
year: 2021
source_url: https://deepmind.google/blog/nowcasting-the-next-hour-of-rain/
tags: [precipitation-nowcasting, deep-generative-model, radar, met-office, uncertainty]
---

# Nowcasting the next hour of rain
**Google DeepMind** · 2021 · [source](https://deepmind.google/blog/nowcasting-the-next-hour-of-rain/)

## Problem
Short-range precipitation forecasting (nowcasting) over the 0-2 hour window is particularly challenging for physics-based NWP models, which struggle to accurately represent convective initiation and storm evolution at fine spatial and temporal scales. Forecasters need probabilistic output that conveys uncertainty rather than a single deterministic trajectory.

## Approach / System design
DeepMind and the UK Met Office developed DGMR (Deep Generative Model of Radar), a deep generative model conditioned on observed radar sequences that produces multiple plausible future precipitation fields for the next two hours. By sampling from the generative model multiple times, DGMR produces a probabilistic ensemble of nowcasts that captures forecast uncertainty at radar resolution.

## Key decisions
Choosing a deep generative approach rather than a regression model allows the system to represent the multi-modal distribution of possible near-term precipitation evolution. Grounding the evaluation in expert meteorologist preference assessments rather than only quantitative metrics ensured that the outputs were judged useful in an operational forecasting context.

## Stack
Deep generative model (DGMR), conditioned on UK Met Office radar composites, collaborative development between DeepMind and the Met Office.

## Results
In a structured evaluation, more than 50 expert meteorologists preferred DGMR's nowcasts over competing methods in 89% of head-to-head comparisons.

## Takeaways
Deep generative models are a natural fit for probabilistic precipitation nowcasting because they can learn the full distribution of possible storm evolutions from radar data. Expert preference evaluations are a valuable complement to quantitative metrics for assessing operational utility in safety-critical forecasting contexts.
