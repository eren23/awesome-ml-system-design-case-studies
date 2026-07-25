---
id: cs2179
title: Advancing Memory Leak Detection with AIOps—Introducing RESIN
company: Microsoft
primary_category: anomaly
sub_category: observability
year: 2024
source_url: https://azure.microsoft.com/en-us/blog/advancing-memory-leak-detection-with-aiops-introducing-resin/
tags: [memory-leak, aiops, azure, heap-analysis, multi-stage-pipeline, cloud-reliability]
---

# Advancing Memory Leak Detection with AIOps—Introducing RESIN
**Microsoft** · 2024 · [source](https://azure.microsoft.com/en-us/blog/advancing-memory-leak-detection-with-aiops-introducing-resin/)

## Problem
Memory leaks in cloud infrastructure are slow-burn faults that degrade performance, crash hosts, and hurt co-located processes. Static leak detection has limited accuracy and scalability (especially for cross-component contract violations), while dynamic instrumentation-based approaches are intrusive and too costly at cloud scale. Before RESIN, leak detection in Azure was fragmented per team.

## Approach / System design
RESIN is a centralized, end-to-end memory leak service running multi-stage detection without needing source code, instrumentation, or recompilation. Lightweight agents collect host-level memory telemetry; a remote service aggregates it using a bucketization-pivot scheme. Detection is two-level: a global bucket-based pivot analysis groups raw memory usage into buckets per component, computes severity scores from deviations and host counts, and runs anomaly detection on each bucket's time series; when a bucket looks leaky, a second-level per-process analysis pinpoints the leaking process with start/end time and severity. For highly suspicious leaks, RESIN takes live heap snapshots (via the Windows heap manager), compares them against periodically fingerprinted reference snapshots, and runs a diagnosis algorithm that outputs root-cause stack traces attached to the alert ticket. Finally it auto-mitigates via a rule-based decision tree: process/service restart first, kernel soft reboot (Project Tardigrade, after live VM migration) next, full OS reboot only as last resort, stopping once the target no longer leaks.

## Key decisions
- Centralized multi-stage pipeline instead of per-team tooling, trading fine-grained always-on profiling for low overhead at global scale.
- Bucketization to tolerate noisy, workload-driven memory usage and cut anomaly-detection compute.
- Expensive heap snapshotting only for prioritized candidates (top three hosts by leak severity, noise level, customer impact), with trigger-based, growth-pattern-aware (steady/spike/stair) collection windows.
- Mitigation escalation ladder chosen to minimize customer impact, reserving reboots for when restarts fail.

## Stack
Host monitoring agents, remote aggregation/analysis service, time-series anomaly detection over bucketized telemetry, Windows heap manager snapshots, reference snapshot database, rule-based mitigation decision tree, Project Tardigrade soft reboots. (Published as an OSDI'22 paper with Johns Hopkins.)

## Results
In production since late 2018, monitoring millions of host nodes and hundreds of host processes daily. 85% precision and 91% recall on leak detection. From September 2020 to December 2023, low-memory VM unexpected reboots dropped nearly 100x and VM allocation error rates dropped over 30x; no severe Azure outages caused by host memory leaks since 2020.

## Takeaways
A staged funnel — cheap coarse telemetry, targeted process analysis, expensive snapshots only when justified — makes leak detection tractable at cloud scale. Making alerts actionable (root-cause stack traces attached to tickets) and closing the loop with automated, impact-minimizing mitigation turns detection into measurable reliability gains.
