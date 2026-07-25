---
id: cs1798
title: Pinpointing Anomalies Along the Path for Network Events
company: Cisco ThousandEyes
primary_category: anomaly
sub_category: root-cause
year: 2025
source_url: https://medium.com/thousandeyes-engineering/pinpointing-anomalies-along-the-path-for-network-events-29736802ea49
tags: [traceroute, per-link-latency, forwarding-vectors, fault-localization, packet-loss]
---

# Pinpointing Anomalies Along the Path for Network Events
**Cisco ThousandEyes** · 2025 · [source](https://medium.com/thousandeyes-engineering/pinpointing-anomalies-along-the-path-for-network-events-29736802ea49)

## Problem
ThousandEyes' Event Detection can tell customers that a network issue exists, but not where along the path it occurred. Network teams still had to manually work out which link or router was responsible for latency spikes and packet loss spanning multiple paths and tests.

## Approach / System design
A proof-of-concept diagnostic pipeline analyzes traceroute data in two parallel streams. The latency stream converts hop-by-hop round-trip times into per-link latencies — link latency between hop i-1 and hop i is RTT(i) minus RTT(i-1) — and compares each per-link time series against a baseline built from pre-event (normal operation) periods to flag anomalous links. The packet-loss stream models each router's forwarding behavior as forwarding vectors over longitudinal sets of traceroutes; deviations between event-window vectors and baseline vectors point to the routers dropping packets.

## Key decisions
- Localize faults by decomposing end-to-end measurements into per-link/per-hop components rather than reasoning over path-level aggregates.
- Establish baselines from pre-event traceroute data so anomalies are judged relative to that path's own normal behavior.
- Combine two independent signals — per-link latency and forwarding-vector shifts — to triangulate the root cause.
- Acknowledge that path asymmetry limits per-link latency accuracy, with future iterations planned to reduce that effect.

## Stack
Not covered in the source beyond the ThousandEyes platform and standard network measurement primitives (traceroute, ping).

## Results
In the illustrative event (06:00-10:30 UTC, roughly 4.5 hours, seen by 10 agents measuring one target), the pipeline flagged link A9, whose latency spiked past 1000 ms during the window, and identified Router A as the root cause — confirmed against the network topology.

## Takeaways
Root-cause localization falls out of decomposition plus baselining: per-link deltas expose what raw end-to-end values hide, and cross-validating latency anomalies with forwarding-pattern shifts gives confidence in blaming a specific router.
