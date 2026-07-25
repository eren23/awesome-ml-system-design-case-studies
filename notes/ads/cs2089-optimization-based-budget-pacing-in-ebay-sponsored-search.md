---
id: cs2089
title: Optimization-Based Budget Pacing in eBay Sponsored Search
company: eBay
primary_category: ads
sub_category: bidding
year: 2024
source_url: https://dl.acm.org/doi/10.1145/3589335.3648331
tags: [budget-pacing, sponsored-search, bid-shading, AdaptivePacing, auction, optimization]
---

# Optimization-Based Budget Pacing in eBay Sponsored Search
**eBay** · 2024 · [source](https://dl.acm.org/doi/10.1145/3589335.3648331)

## Problem
In eBay's automated sponsored search auctions, campaigns that always bid their maximum risk exhausting budgets early and missing high-traffic, high-response periods later in the day. The platform needs pacing that keeps seller spending smooth without sacrificing impressions/clicks. Prior pacing work is split between empirical heuristics (throttling, PID controllers) and theoretical methods whose assumptions (stationarity, asymptotic horizons) fail in a noisy real marketplace.

## Approach / System design
The team took AdaptivePacing — a bid-shading algorithm derived from the Lagrangian dual of the advertiser's utility-maximization problem under a budget constraint — and integrated it into eBay's sponsored search setting. Each campaign posts bid v/(1+μ), where the pacing multiplier μ is updated each round by subgradient descent on the gap between realized spend and a target spending curve (ρ·B per round). Evaluation ran on eBay's counterfactual simulation test bed built from historical search requests over a one-day horizon (T=1440 one-minute rounds), against no-pacing, Throttling, and PID-controller baselines. They also proposed variants: AdaptivePacing-SpendingPenalty (a second "spending multiplier" γ enforcing a minimum-spending constraint so platform revenue doesn't drop too far) and heuristics that pace only some campaigns — by budget threshold (AdaptivePacing-Budget), click opportunities (AdaptivePacing-Click), time of day (AdaptivePacing-Time), and prior budget-depletion share (AdaptivePacing-BudgetSpent).

## Key decisions
- Bid shading over throttling: moderate bid amounts instead of probabilistically excluding campaigns from auctions, so campaigns can still seize opportunities.
- Target spending curves (traffic, uniform, CTR) are configurable per campaign rather than forcing uniform pacing; the traffic curve worked best overall.
- Add a minimum-spending constraint (dual variable γ) to balance advertiser utility against the platform's revenue objective; step sizes ε, ε′ encode that trade-off.
- Restrict pacing to campaigns with binding budget constraints (e.g., those that historically deplete budgets) rather than pacing everyone.
- They show AdaptivePacing is a special case of a dual-based PID controller (P-only), connecting theory to the widely used industry heuristic.

## Stack
eBay's sponsored search counterfactual simulator ("sponsored search gym") replaying logged search/auction data with second-price multi-slot auctions; subgradient-descent dual updates; comparisons vs. throttling and dual-based PID controllers. No specific ML frameworks covered in the source.

## Results
Relative to no-pacing (traffic curve): +6.21% impressions, +5.48% clicks, +6.01% surface rate, −10.20% CPC, −18.72% pacing error, with revenue −5.39% (the advertiser-vs-platform trade-off). Throttling instead lost impressions/clicks (−0.45%, −1.10%) despite the best pacing error (−51.62%). Pacing only campaigns that fully depleted their budget (AdaptivePacing-BudgetSpent, PS≥100%) gave the best overall profile: +6.48% impressions, +5.73% clicks with revenue only −1.96%. Dual-based PID with bid factor 1/(1+μ) performed best among PID variants (+5.99% imps, +5.52% clicks).

## Takeaways
Theory-derived pacing transfers to a noisy real marketplace even when its assumptions don't hold; bid shading beats throttling on advertiser-facing metrics; the platform-revenue dip from shading can be managed with minimum-spending constraints or by pacing only budget-binding campaigns; and PID pacing heuristics are best understood as extensions of the dual optimization framework.
