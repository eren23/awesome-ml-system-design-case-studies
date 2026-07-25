---
id: cs2370
title: The Role of Anomaly Detection in IAM
company: Capital One
primary_category: anomaly
sub_category: outlier-detection
year: 2023
source_url: https://www.capitalone.com/tech/software-engineering/anomaly-detection-iam/
tags: [identity-access-management, anomaly-detection, ML, access-control, security, observability]
---

# The Role of Anomaly Detection in IAM
**Capital One** · 2023 · [source](https://www.capitalone.com/tech/software-engineering/anomaly-detection-iam/)

## Problem
Traditional rule-based fraud and access controls are reactive — they fire only on known immediate threats. They miss the quieter signals: security rules that go dormant, unexplained drops in verification usage, or gradual behavioral drift that precedes an attack. As fraudsters grow more sophisticated, the harder problem becomes detecting what *isn't* triggering, not just what is.

## Approach / System design
Capital One layered ML-driven anomaly detection on top of its identity and access management (IAM) telemetry:
- Baseline comparison of current behavior against historical patterns to flag deviations.
- Contextual ML models that factor in time of day, geography, device type, and user segment to cut false positives.
- Change point detection to catch gradual behavioral shifts before they escalate.
- Continuous "intent = execution" validation, auditing that identity systems actually behave as designed across the identity lifecycle.
Identity logs, metadata, and behavioral data are consolidated into a unified observability layer that feeds these detectors.

## Key decisions
- Shifted from reactive alerting to proactive monitoring across multiple signal types, including absence-of-activity signals.
- Used ML to contextualize changes rather than firing on raw thresholds.
- Treated abandonment rates as security indicators alongside traditional fraud metrics.
- Unified identity telemetry into a single layer instead of siloed logs.

## Stack
ML models for behavioral baselining and contextual analysis; a unified telemetry/observability layer for logs, metadata, and behavioral data; automated governance for rule auditing. Specific tooling is not named in the source.

## Results
The article stays qualitative: detecting silent failures (like dormant rules), surfacing blind spots in access-rule coverage, and validating that execution matches intent. No concrete performance numbers are given.

## Takeaways
Anomaly detection in IAM is as much about auditing your own controls as catching attackers — dormant rules and missing signals are risks too. Contextual ML baselines reduce alert noise, and unified identity telemetry is the prerequisite for seeing the unseen while preserving a seamless customer experience.
