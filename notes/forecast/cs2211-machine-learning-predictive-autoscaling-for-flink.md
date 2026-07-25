---
id: cs2211
title: Machine-Learning Predictive Autoscaling for Flink
company: Grab
primary_category: forecast
sub_category: time-series
year: 2025
source_url: https://engineering.grab.com/ml-predictive-autoscaling-for-flink
tags: [flink, autoscaling, time-series, kafka, capacity-planning, streaming, workload-forecasting, seasonal-patterns]
---

# Machine-Learning Predictive Autoscaling for Flink
**Grab** · 2025 · [source](https://engineering.grab.com/ml-predictive-autoscaling-for-flink)

## Problem
Grab's Flink stream-processing footprint grew 2.5x in a year, and teams were manually sizing CPU/memory, leading to over-provisioning and waste. Reactive autoscaling via Kubernetes HPA made things worse: whenever a job restarted from a checkpoint it reprocessed backlogged records, spiking CPU (0.5 to 2.5 cores) and latency (up to ~3 minutes) even though real source throughput hadn't changed. Misconfigured HPA thresholds plus these restart spikes created self-amplifying feedback loops — in one case a pipeline restarted 6 times in 30 minutes. Kafka partition counts also capped horizontal parallelism.

## Approach / System design
A Predictive Resource Advisor works in four stages: (1) a time-series forecasting model trained on Kafka source-topic throughput captures seasonal patterns and organic growth; (2) a regression model maps input workload to required CPU (Ct = f(xt)), trained only on data from stable operating periods; (3) the forecaster projects load for the next t-hour window; (4) the predicted workload feeds the resource model, safety adjustments are applied, and a custom autoscaler controller performs vertical scaling. This replaces reactive HPA for Flink workloads: capacity is adjusted ahead of demand instead of in response to degradation.

## Key decisions
- Vertical scaling (more CPU per TaskManager) rather than horizontal, because fixed Kafka partition counts limit parallelism.
- Kafka throughput chosen as the model input since it reflects true business demand and is independent of Flink consumer behavior.
- Restart-spike anomalies and unstable periods excluded from training data to prevent inflated CPU estimates and feedback loops.
- Predictive over reactive scaling so systems are prepared before demand arrives, avoiding artificial load from checkpoint reprocessing.

## Stack
Kubernetes, Flink (Application Mode), Kafka, a custom autoscaler controller replacing HPA, plus in-house time-series forecasting and regression models (frameworks not specified).

## Results
Rolled out to over 50% of applicable production applications (Kafka-sourced jobs with seasonal patterns), yielding roughly >35% cloud infrastructure cost savings by aligning CPU with low-traffic periods. Scaling became deterministic and less disruptive; in an experimental pipeline, nine autoscaling-induced restarts produced latency spikes peaking just over four minutes, comparable to the pre-existing ~3-minute restart baseline, while a statically provisioned control pipeline stayed sub-second with no disruptions.

## Takeaways
Predictive scaling tied to a business-demand signal (Kafka throughput) delivers both cost savings and stability, and removes manual tuning burden. The approach fits Kafka-sourced, seasonal workloads; bursty or non-Kafka jobs remain open problems. Future work includes memory configuration (OOMKill prevention), anomaly detection for bursty patterns, and pretrained/LLM-based time-series forecasting to cut training effort.
