---
id: cs2182
title: Get Notified About the Most Relevant Events with Advanced HTTP Alerts
company: Cloudflare
primary_category: anomaly
sub_category: alerting
year: 2025
source_url: https://blog.cloudflare.com/custom-alert-features-anomaly-detection/
tags: [http-alerting, traffic-anomaly, statistical-threshold, z-score, slo-alerting]
---

# Get Notified About the Most Relevant Events with Advanced HTTP Alerts
**Cloudflare** · 2025 · [source](https://blog.cloudflare.com/custom-alert-features-anomaly-detection/)

## Problem
Cloudflare's HTTP alerting was too generic: customers could only pick which Internet properties to watch and a sensitivity level. They couldn't exclude their own test IPs, monitor specific paths, filter by HTTP status codes, or monitor a whole account versus individual zones — so alerts fired on irrelevant events and missed the questions customers actually had ("Which HTTP errors are crossing my SLO threshold? Is this spike my own internal testing?").

## Approach / System design
Advanced HTTP Alerts reuse the request metadata already flowing through Cloudflare's network to drive customizable anomaly alerting. The system detects anomalous events such as spikes in origin error rates so customers can investigate and mitigate proactively. Per the catalog metadata, the anomaly detection compares 5-minute traffic windows against 4-hour baselines and fires when deviations exceed 3.5 standard deviations. Alerts are configurable along several dimensions: origin response status codes, edge response status codes, sensitivity/SLO targets, client IPv4/IPv6 addresses, and specific zones.

## Key decisions
- Build alert customization on metadata already collected at the edge rather than new instrumentation.
- Statistical short-window-vs-baseline comparison instead of static thresholds, with user-configurable sensitivity tied to SLO targets.
- Filters for excluding known traffic (e.g., a customer's own test IPs) to cut false positives at the source.
- Account-level and zone-level scoping; management through the notification dashboard with account-level privileges required.

## Stack
Cloudflare edge network request metadata, notification management dashboard. Feature available to Enterprise customers.

## Results
Not covered in the source (no adoption or noise-reduction metrics stated).

## Takeaways
Anomaly alerting becomes useful when customers can shape both the statistical sensitivity and the traffic slice it applies to; letting users filter by status code, IP, and SLO turns a generic spike detector into an answer to specific operational questions.
