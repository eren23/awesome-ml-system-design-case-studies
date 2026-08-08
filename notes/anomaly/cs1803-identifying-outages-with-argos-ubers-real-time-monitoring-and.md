---
id: cs1803
title: Identifying Outages with Argos, Uber's Real-Time Monitoring and Root-Cause Exploration Tool
company: Uber
primary_category: anomaly
sub_category: root-cause
year: 2015
source_url: https://www.uber.com/blog/argos-real-time-alerts/
tags: [argos, dynamic-thresholds, outlier-detection, alert-fatigue, health-index]
---

# Identifying Outages with Argos, Uber's Real-Time Monitoring and Root-Cause Exploration Tool
**Uber** · 2015 · [source](https://www.uber.com/blog/argos-real-time-alerts/)

## Problem
Uber needed real-time visibility into the health of its rapidly growing platform, where metric spikes can result from legitimate demand increases (e.g., surge pricing events) or genuine service outages. Static thresholds generated excessive false positives during demand spikes, and once an alert fired, there was no automated mechanism to help engineers identify which downstream metrics were causally related to the anomaly.

## Approach / System design
Argos uses a two-stage detection pipeline: a fast outlier detector provides near-real-time anomaly flags, while a heavier detection pass runs hourly using dynamic thresholds computed from historical metric distributions. A System Health Index (SHI) aggregates metric dependency relationships, allowing Argos to distinguish genuine outages — where multiple dependent metrics degrade together — from isolated demand-driven spikes that affect only superficially correlated signals.

## Key decisions
The two-stage architecture trades off detection speed against accuracy: the fast stage minimizes time-to-alert while the hourly pass reduces false positives. Building the SHI as a metric dependency graph reflects the insight that outages have a distinctive multi-metric signature that demand spikes do not, providing a principled way to reduce alert fatigue.

## Stack
Custom real-time monitoring platform (Argos), dynamic threshold computation, outlier detection algorithms, System Health Index dependency graph.

## Results
Not covered in the source.

## Takeaways
Dynamic thresholds that adapt to historical metric baselines substantially reduce false positive rates compared to static thresholds, particularly for services with large demand variation. A two-stage detection pipeline — fast but noisy followed by slow but precise — allows teams to tune the trade-off between latency and false positive rate. Encoding metric dependency relationships enables automated root-cause hypothesis generation, which speeds up incident investigation and reduces the cognitive load on on-call engineers.
