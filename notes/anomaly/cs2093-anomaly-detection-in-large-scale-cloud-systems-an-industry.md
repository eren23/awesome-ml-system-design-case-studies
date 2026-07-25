---
id: cs2093
title: "Anomaly Detection in Large-Scale Cloud Systems: An Industry Case and Dataset"
company: IBM
primary_category: anomaly
sub_category: outlier-detection
year: 2024
source_url: https://arxiv.org/abs/2411.09047
tags: [cloud-telemetry, multivariate, ibm-cloud, time-series, dataset, icse-seip]
---

# Anomaly Detection in Large-Scale Cloud Systems: An Industry Case and Dataset
**IBM** · 2024 · [source](https://arxiv.org/abs/2411.09047)

## Problem
As cloud systems grow more complex, detecting anomalies in their telemetry becomes critical for reliability — but the research community lacks large-scale, real-world datasets to benchmark detection methods against, so most published techniques are validated on synthetic or small benchmarks that don't reflect production conditions.

## Approach / System design
IBM presents an industry case study of anomaly detection over production telemetry from the IBM Cloud Console. The team collected high-dimensional monitoring data over a 4.5-month window and applied machine learning models for anomaly detection on it, documenting the practical challenges of doing this in a live cloud environment. Alongside the case study, they release the dataset itself as a research artifact.

## Key decisions
- Release real production telemetry rather than synthetic benchmarks, giving researchers a realistic, high-dimensional problem space.
- Frame the contribution as both an industry experience report and a reusable dataset, targeting the practice-oriented ICSE SEIP track.
- Ship a reproducibility package (added in the paper's second version) so results can be replicated.

## Stack
IBM Cloud production telemetry (IBM Cloud Console monitoring); machine learning anomaly detection models applied over multivariate time-series data. Specific model/tooling details are not covered in the abstract.

## Results
- Dataset: 39,365 rows × 117,448 columns of telemetry collected over 4.5 months from IBM Cloud.
- Demonstrated ML-based anomaly detection on this data and catalogued real-world implementation challenges.
- Peer-reviewed: accepted to ICSE SEIP 2025 (47th International Conference on Software Engineering, Software Engineering in Practice track).

## Takeaways
- Production cloud telemetry is extremely high-dimensional (117K+ features), which is a fundamentally different regime than most academic anomaly-detection benchmarks.
- Publishing real operational datasets with reproducibility packages is one of the highest-leverage contributions industry can make to close the research–practice gap in cloud reliability.
