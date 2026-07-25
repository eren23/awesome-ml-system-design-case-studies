---
id: cs2177
title: "Building Unique, Per-Customer Defenses Against Advanced Bot Threats in the AI Era"
company: Cloudflare
primary_category: anomaly
sub_category: outlier-detection
year: 2025
source_url: https://blog.cloudflare.com/per-customer-bot-defenses/
tags: [bot-detection, per-customer-models, behavioral-baseline, seasonality, traffic-anomaly, anomaly-detection, per-customer-model, behavioral-ml, real-time, traffic-analysis]
---

# Building Unique, Per-Customer Defenses Against Advanced Bot Threats in the AI Era
**Cloudflare** · 2025 · [source](https://blog.cloudflare.com/per-customer-bot-defenses/)

## Problem
One-size-fits-all bot detection fails against modern AI-powered scrapers engineered to blend into legitimate traffic — AI-driven scraping accounts for nearly 80% of all AI bot activity on Cloudflare's network. Global signatures and a single network-wide bot score miss attacks that are only anomalous relative to a specific site's normal traffic.

## Approach / System design
Individualized ML models per bot-management customer, running a three-step behavioral anomaly detection pipeline:
1. **Dynamic baselines** — continuously updated "normal" traffic profiles per customer zone that incorporate seasonality and legitimate traffic spikes.
2. **Anomaly identification** — flag deviations contextual to that website's own patterns rather than global signatures.
3. **Actionable findings** — surface new Bot Detection IDs and feed the Bot Score so detections translate into immediate mitigation via existing WAF and security tooling.
Detection combines multiple signal types: HTTP/2 fingerprints, TLS Client Hello extensions, JA4 fingerprints, and behavioral/access-pattern analysis; residential proxy detection combines network data with client-side fingerprints from challenge solves.

## Key decisions
- Strict per-customer isolation: one customer's zone data is never used to train another customer's model.
- Content-agnostic detection — analyze access patterns, not page content, for scalability and privacy.
- Integrate outputs into the existing Bot Score / WAF / Security Analytics surface rather than a parallel enforcement system.
- Complement ML with 50 analyst-written heuristics.

## Stack
Per-customer ML models on Cloudflare's edge network, integrated with Bot Management (Bot Score, Bot Detection IDs), WAF, and Security Analytics.

## Results
- 11 billion requests from residential/commercial proxy networks identified in a 7-day sample.
- 138 million scraping requests flagged in 24 hours across 5 beta zones.
- 34% of flagged requests were undetectable by the existing global bot score system.

## Takeaways
Against adaptive, AI-assisted scrapers, personalization beats global intelligence: per-customer behavioral baselines caught a third more malicious traffic than the aggregate system could see, while data isolation kept the per-customer approach privacy-clean.
