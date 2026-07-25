---
id: cs2119
title: "Introducing Ti2: The Next Generation of Plaid Protect's Trust Index"
company: Plaid
primary_category: fraud
sub_category: payment-fraud
year: 2025
source_url: https://plaid.com/blog/plaid-protect-trust-index/
tags: [trust-scoring, graph-signals, bank-transaction-history, real-time, fraud-detection]
---

# Introducing Ti2: The Next Generation of Plaid Protect's Trust Index
**Plaid** · 2025 · [source](https://plaid.com/blog/plaid-protect-trust-index/)

## Problem
Fraud tactics evolve continuously — synthetic identities, account takeovers, and coordinated fraud rings that spread activity across multiple apps — and detection tools scoped to a single platform cannot see the cross-app patterns that give these schemes away.

## Approach / System design
Ti2 is the second generation of Plaid Protect's Trust Index, an ML-powered fraud scoring model built on signals from Plaid's bank data network. Two major upgrades define this generation: analysis of bank account transaction history, which distinguishes authentic spending behavior from fraud markers such as unusual peer-to-peer transfers and rapid fund cycling; and user graph insights, which surface fraud rings by analyzing shared risk across users, devices, accounts, and apps network-wide.

## Key decisions
- Integrate real-time graph-based features directly into the scoring model instead of treating network signals as separate, bolt-on checks.
- Use bank transaction history as a behavioral trust signal, contextualizing individual transactions within longer-term patterns.
- Prioritize rapid model iteration as a design principle, since staying ahead of fraud tactics matters more than any single model version.

## Stack
Not specified in the article.

## Results
Ti2 catches 30% more fraud than Ti1. In customer-specific evaluations: a digital lender could detect 40% of first-party fraud while flagging only 5% of users; a cash advance service would flag 1 in 10 users to catch 43% more fraud; a crypto firm could prevent 50% of fraud losses.

## Takeaways
Fraud that is invisible within one app becomes visible when individual transactions are contextualized against broader user behavior and cross-app network structure. Network position — seeing many apps and institutions at once — is itself the detection advantage.
