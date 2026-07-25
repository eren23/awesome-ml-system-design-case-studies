---
id: cs1796
title: "Measuring ISP Health: City-scale Outage and Timing Anomaly Detection"
company: Cisco ThousandEyes
primary_category: anomaly
sub_category: outlier-detection
year: 2025
source_url: https://medium.com/thousandeyes-engineering/measuring-isp-health-city-scale-outage-and-timing-anomaly-detection-4f6bccb534e2
tags: [network-monitoring, outage-detection, time-series, router-agents, baselines]
---

# Measuring ISP Health: City-scale Outage and Timing Anomaly Detection
**Cisco ThousandEyes** · 2025 · [source](https://medium.com/thousandeyes-engineering/measuring-isp-health-city-scale-outage-and-timing-anomaly-detection-4f6bccb534e2)

## Problem
Traditional network monitoring is reactive — alerts arrive only after users are already degraded. ThousandEyes wanted to proactively detect performance problems affecting thousands of users in a city, and to attribute them correctly: is the fault in the ISP, a specific CDN, or somewhere on the path?

## Approach / System design
Agents embedded in home routers run scheduled performance measurements. A fully automated pipeline analyzes the data in time buckets and classifies events into three types: ISP-wide events (multiple CDNs degraded across agents), CDN-specific events (only one CDN affected), and partial ISP-wide events (regional point-of-presence issues hitting a small fraction of users). Outage detection computes a failure rate — the ratio of agents with missing measurements to total deployed agents — and runs time-series anomaly detection comparing the current window against historical baselines. Timing anomaly detection independently analyzes per-stage metrics (DNS lookup, connect time, total fetch time), tracking samples marked "normal" over a set number of preceding hours and applying statistical-significance testing to flag shifts, which isolates which stage of the transaction the problem lives in.

## Key decisions
- Use home-router agents as the vantage point, giving city-scale coverage from real subscriber locations.
- Separate outage detection (failure rates) from timing-anomaly detection (per-stage latency shifts) as independent signals.
- Attribute events by cross-CDN pattern: multiple CDNs affected implies ISP fault, single CDN implies CDN fault.
- Baseline against recent "normal" history rather than fixed thresholds.

## Stack
Not covered in the source beyond time-series analysis and statistical distribution-comparison methods on the ThousandEyes platform.

## Results
Detected the July 24, 2025 Starlink outage as an ISP-wide failure with failure rates approaching 100% starting at 19:13 UTC, against baseline failure rates of about 20% during peak utilization; the measured 2.5-hour duration matched external reports. Also caught an ISP-wide timing anomaly with latency inflation across multiple targets lasting 1 hour 25 minutes.

## Takeaways
Proactive, baseline-relative detection from in-home vantage points lets ISPs learn about outages at onset instead of after complaints, cutting MTTR; the same signals can later drive SLA-violation tracking and automated remediation.
