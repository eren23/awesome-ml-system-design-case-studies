---
id: cs2120
title: "Ti3 is Here: A Bigger Graph for a Fast Moving Fraud Landscape"
company: Plaid
primary_category: fraud
sub_category: risk-scoring
year: 2026
source_url: https://plaid.com/blog/introducing-trust-index-3-fraud-detection/
tags: [graph-ml, fraud-graph, real-time, trust-scoring, network-analysis]
---

# Ti3 is Here: A Bigger Graph for a Fast Moving Fraud Landscape
**Plaid** · 2026 · [source](https://plaid.com/blog/introducing-trust-index-3-fraud-detection/)

## Problem
Fraud detection confined to a single platform misses coordinated rings that deliberately distribute their activity across many institutions and accounts. Fraudsters exploit that fragmentation — no individual app sees enough of the picture to flag them.

## Approach / System design
Ti3, the third generation of Plaid's Trust Index, is built around a dramatically expanded fraud graph mapping relationships among devices, accounts, identities, sessions, and institutions. The graph grew roughly 10x within months and can be traversed up to nine hops deep in real time, uncovering multi-degree fraud connections. It targets patterns such as rapid multi-platform account opening, shared infrastructure linking supposedly unrelated identities, repeated account linking/disconnection cycles, geographic inconsistencies between IP location and registered address, and deviations from a user's established behavior. Nearly one million daily Plaid connections feed the model.

## Key decisions
- Network-based architecture over single-platform models — the graph is the product.
- Enhanced device identification through Plaid Link integration, positioned as significantly harder to bypass than traditional device fingerprinting.
- Improved account age detection by combining bank account history, transaction patterns, and network relationships.
- Expanded signal categories so customers get clearer, more actionable risk insights.

## Stack
Not specified in the article beyond the fraud graph and Plaid Link integration.

## Results
Ti3 catches up to 41% more fraud at the same false positive rate, powered by an approximately 10x graph expansion and real-time traversal up to nine hops deep, with nearly one million daily connections feeding the model.

## Takeaways
Ecosystem-wide network visibility compounds: each generation of the graph widens what any single customer could see alone, and that data-network advantage is structurally hard for platform-scoped competitors to replicate. Deep real-time graph traversal turns multi-degree, cross-institution relationships into a first-class fraud signal.
