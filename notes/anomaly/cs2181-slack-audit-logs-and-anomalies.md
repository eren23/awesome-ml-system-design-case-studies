---
id: cs2181
title: Slack Audit Logs and Anomalies
company: Slack
primary_category: anomaly
sub_category: observability
year: 2024
source_url: https://slack.engineering/slack-audit-logs-and-anomalies/
tags: [audit-logs, enterprise-security, dynamic-thresholds, per-organization-calibration, automated-response]
---

# Slack Audit Logs and Anomalies
**Slack** · 2024 · [source](https://slack.engineering/slack-audit-logs-and-anomalies/)

## Problem
Enterprise security teams need to spot suspicious activity in Slack workspaces (compromised accounts, data exfiltration, API abuse), but raw audit logs are extremely high volume and require heavy investigation effort to separate genuine threats from noise.

## Approach / System design
Slack runs a dual-layer system: comprehensive audit logs record all platform actions, and automated anomaly detection pipelines flag unusual patterns (e.g., anomalous user agents, excessive downloads, unusual IPs/Tor access). Anomalies flow through the same Audit Logs API event stream as regular events but carry a distinct "anomaly" action type, so customers can consume them via the same integrations. Detections are surfaced as indicators for investigation rather than auto-escalated incidents, and organizations can correlate multiple anomaly types together (e.g., user_agent + excessive_downloads + ip_address pointing to account compromise) and respond via session-termination endpoints.

## Key decisions
- Treat anomalies as investigation prompts, not incidents — each organization judges relevance against its own security policies.
- Encourage correlation of multiple related anomalies over reacting to single signals.
- Support aggregation so organizations can compare anomaly frequency against historical norms to catch emerging threats.
- Provide allowlisting of CIDR ranges and ASNs (allowlists over blocklists) to suppress false positives from known-legitimate sources.

## Stack
Audit Logs API with filtering, anomaly event type in the audit stream, web dashboard (Tools and Settings), session-termination endpoints, and third-party SIEM integrations including Splunk, AWS AppFabric, and Datadog.

## Results
Anomaly logs run at least two orders of magnitude lower volume than full audit logs, making focused monitoring feasible while the full audit stream preserves investigation context.

## Takeaways
Consume complete audit logs where possible to maximize investigative context; use allowlists rather than blocklists for unexpected user agents; and correlate multiple signal types before escalating. A low-volume, curated anomaly stream layered on top of raw logs gives security teams signal without drowning them.
