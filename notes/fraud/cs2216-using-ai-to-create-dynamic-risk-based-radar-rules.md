---
id: cs2216
title: Using AI to Create Dynamic, Risk-Based Radar Rules
company: Stripe
primary_category: fraud
sub_category: payment-fraud
year: 2025
source_url: https://stripe.com/blog/using-ai-dynamic-radar-rules
tags: [rule-engine, adaptive-rules, radar, payment-fraud, real-time-ml, issuer-signals]
---

# Using AI to Create Dynamic, Risk-Based Radar Rules
**Stripe** · 2025 · [source](https://stripe.com/blog/using-ai-dynamic-radar-rules)

## Problem
Stripe Radar's historical approach used binary rules: automatically block a transaction if the card verification code (CVC) or postal-code check failed. These blanket rules declined many legitimate payments — customers mistype CVCs and postal codes — reducing payment success rates and costing businesses revenue.

## Approach / System design
The new adaptive rules combine Stripe's ML risk scoring with the card issuer's own decision data. The flow: (1) Stripe's models produce a fraud risk score from patterns learned across millions of businesses and tens of billions of transactions; (2) the transaction routes to the issuer for authorization; (3) the issuer returns its decision plus verification responses (e.g., CVC mismatch flagged); (4) Radar combines the original risk score with the issuer's response to make the final allow/block decision. Low-risk transactions with a failed CVC or postal check are now authorized; high-risk ones remain blocked. Through the Enhanced Issuer Network, issuers can also consume Radar's fraud scores to improve their own authorization decisions.

## Key decisions
- Replace binary verification-failure blocks with risk-based decisions that weigh the ML score against the issuer's signals.
- Collaborate bidirectionally with issuers (Enhanced Issuer Network) rather than treating authorization as a black box.
- Run the new adaptive rules independently alongside businesses' existing Radar rule configurations, so migration doesn't interfere with current setups.

## Stack
Stripe's Radar ML risk-scoring models and real-time decisioning infrastructure coordinating with card networks and issuers. The post does not detail specific technologies.

## Results
Businesses that migrated saw a 1.3 percentage-point increase in payment success rates while fraud detection rates were maintained; across Stripe's customer base this could translate to billions of dollars of additional annual revenue.

## Takeaways
Static rules discard context that other participants in the payment flow already have. Fusing internal ML risk scores with external issuer decisioning data produces more nuanced fraud decisions — recovering legitimate revenue without giving ground on fraud.
