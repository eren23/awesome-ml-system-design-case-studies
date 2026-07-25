---
id: cs1799
title: "DrP: Meta's Root Cause Analysis Platform at Scale"
company: Meta
primary_category: anomaly
sub_category: root-cause
year: 2025
source_url: https://engineering.fb.com/2025/12/19/data-infrastructure/drp-metas-root-cause-analysis-platform-at-scale/
tags: [incident-response, anomaly-detection, time-series-correlation, dimension-analysis, mttr]
---

# DrP: Meta's Root Cause Analysis Platform at Scale
**Meta** · 2025 · [source](https://engineering.fb.com/2025/12/19/data-infrastructure/drp-metas-root-cause-analysis-platform-at-scale/)

## Problem
Investigating incidents in Meta's deeply interconnected systems was manual, slow, and error-prone: on-call engineers leaned on outdated playbooks and ad-hoc scripts, which prolonged downtime and drove on-call fatigue.

## Approach / System design
DrP is an end-to-end root-cause-analysis automation platform with four parts. An expressive, type-safe SDK lets engineers author investigation workflows ("analyzers") using helper libraries and ML algorithms for anomaly detection, event isolation, time-series correlation, and dimension analysis. A scalable multi-tenant backend manages queues and worker pools to execute analyzers securely and distributed, delivering results asynchronously. Workflow integration ties DrP into alerting and incident-management tooling so analyses auto-trigger on incidents. A post-processing system takes automated mitigation actions from findings, such as creating tasks or pull requests. An insights system additionally identifies and ranks the top causes behind alerts.

## Key decisions
- Ship RCA as an SDK engineers program against, rather than a fixed set of built-in investigations.
- Make the SDK type-safe to capture investigation context reliably.
- Support analyzer chaining so investigations can follow dependencies across services.
- Run automated backtesting during code review to keep analyzer quality high.
- Auto-trigger analyses from alerts and close the loop with automated mitigation actions.

## Stack
The article describes ML algorithms (anomaly detection, event isolation, time-series correlation, dimension analysis) but names no specific frameworks or tools.

## Results
In production for over 5 years: adopted by 300+ teams, with about 2,000 analyzers deployed and roughly 50,000 analyses executed daily. MTTR reductions of 20-80% across use cases.

## Takeaways
Turning incident investigation into code — an SDK with reusable ML analysis primitives, auto-triggered from alerts and backtested in review — scales institutional debugging knowledge across an organization and measurably cuts resolution time while easing on-call burden.
