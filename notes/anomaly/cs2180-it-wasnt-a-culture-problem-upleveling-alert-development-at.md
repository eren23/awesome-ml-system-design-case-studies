---
id: cs2180
title: "It Wasn't a Culture Problem: Upleveling Alert Development at Airbnb"
company: Airbnb
primary_category: anomaly
sub_category: alerting
year: 2026
source_url: https://medium.com/airbnb-engineering/it-wasnt-a-culture-problem-upleveling-alert-development-at-airbnb-01e2290eb0f5
tags: [observability-as-code, alerting, burn-rate, change-detection, backtesting, alert-noise-reduction]
---

# It Wasn't a Culture Problem: Upleveling Alert Development at Airbnb
**Airbnb** · 2026 · [source](https://medium.com/airbnb-engineering/it-wasnt-a-culture-problem-upleveling-alert-development-at-airbnb-01e2290eb0f5)

## Problem
Airbnb manages 300,000 production alerts but had no good way to validate an alert change before deploying it. Code review and dashboard eyeballing couldn't predict how an alert would actually behave, so engineers ran weeks-long side-by-side production deployments to test changes. The result: noisy alerts eroded trust, and engineers avoided iterating because they couldn't predict the impact — a workflow gap that looked, misleadingly, like a culture problem.

## Approach / System design
An Observability-as-Code platform with local-first alert development, rolled out in three phases:
1. **Text-based diffs** — Markdown alert diffs with field-level granularity and links to the underlying queries, for review in CI.
2. **Change Report UI** — side-by-side visualization of a proposed alert against its production state.
3. **Bulk backtesting** — simulate proposed alerts against historical data by running them through Prometheus's own rule manager, computing "noisiness" metrics that prioritize which changes need human review.
On top of the workflow, the platform ships higher-level alert abstractions: anomaly detection, burn-rate alerts, and change-detection patterns.

## Key decisions
- Compatibility over novelty: use Prometheus rule groups as the standard input format and hook into Prometheus's real rule-evaluation engine for backtests instead of reimplementing evaluation semantics; expose results via the standard query API.
- Guardrails for backtesting at scale: each backtest runs in isolated Kubernetes pods with autoscaling, concurrency limits, error thresholds, and multiple circuit breakers.
- Own the full surface — input language, generation, UI, and validation tooling — to control developer experience end to end.
- Ship incomplete-but-usable phases early with good UX guidance rather than waiting on a complete platform.

## Stack
Prometheus (rule manager, rule groups, query API), Kubernetes, CLI tooling, CI integration.

## Results
- 300,000 alerts migrated from a vendor system to Prometheus.
- Alert development cycles collapsed from weeks to minutes.
- Companywide alert noise reduced by 90%.

## Takeaways
What looked like an alerting culture problem was a missing feedback loop: once engineers could see, pre-deployment, exactly how an alert would have fired historically, iteration became cheap and noise fell 90%. Reusing the monitoring system's own evaluation engine for backtesting bought correctness for free.
