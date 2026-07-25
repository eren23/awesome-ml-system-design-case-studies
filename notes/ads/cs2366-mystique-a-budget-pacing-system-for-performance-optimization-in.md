---
id: cs2366
title: "Mystique: A Budget Pacing System for Performance Optimization in Online Advertising"
company: Yahoo
primary_category: ads
sub_category: budget-pacing
year: 2024
source_url: https://www.yahooinc.com/research/publications/mystique-a-budget-pacing-system-for-performance-optimization-in-online-advertising
tags: [budget-pacing, soft-throttling, spending-curve, native-advertising, programmatic, production-system, pacing-signal]
---

# Mystique: A Budget Pacing System for Performance Optimization in Online Advertising
**Yahoo** · 2024 · [source](https://www.yahooinc.com/research/publications/mystique-a-budget-pacing-system-for-performance-optimization-in-online-advertising)

## Problem
Advertisers allocate campaign budgets that compete for placements in first-price auctions. Treating each auction as an isolated event with greedy spending leads to suboptimal patterns — budgets can deplete too early and miss better opportunities later in the day. Yahoo needed a systematic way to pace campaign spend across the day in its native advertising marketplace.

## Approach / System design
Mystique is a "soft" throttling-based budget pacing system operating at two levels. First, it establishes a daily target spending curve per campaign, informed by historical spending data. Second, it continuously updates a pacing signal that keeps actual spend aligned with that curve. Instead of hard throttling — probabilistically excluding a campaign from auctions — the pacing signal acts as a multiplicative factor on bids, so campaigns stay in every auction with adjusted bid amounts.

## Key decisions
- Chose soft throttling (bid multiplication) over hard throttling (random auction exclusion), letting campaigns participate in all auctions while still controlling spend.
- Split the architecture into two tiers: daily target-curve construction versus continuous real-time pacing-signal updates.
- Optimized for depleting budgets smoothly while securing more high-value opportunities across the day.

## Stack
Not covered in the source.

## Results
- Deployed in production for multiple years in Yahoo's native advertising marketplace.
- Paces over $1 billion USD of ad spend annually.
- Offline evaluation in a simulated marketplace showed it outperformed baseline pacing algorithms.

## Takeaways
Adaptive, signal-based pacing that adjusts bids beats exclusionary throttling: it preserves auction participation, spends budgets more smoothly, and optimizes performance rather than merely capping expenditure.
