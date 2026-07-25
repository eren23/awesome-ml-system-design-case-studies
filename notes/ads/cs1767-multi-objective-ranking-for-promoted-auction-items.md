---
id: cs1767
title: Multi-Objective Ranking for Promoted Auction Items
company: eBay
primary_category: ads
sub_category: auction
year: 2022
source_url: https://medium.com/@ebaytechblog/multi-objective-ranking-for-promoted-auction-items-293bf204574f
tags: [promoted-listings, ranking, logistic-regression, epsilon-greedy]
---

# Multi-Objective Ranking for Promoted Auction Items
**eBay** · 2022 · [source](https://medium.com/@ebaytechblog/multi-objective-ranking-for-promoted-auction-items-293bf204574f)

## Problem
eBay's Promoted Listings Express (PLX) shows promoted auction items in fixed "Similar Sponsored Items" slots. The ranking has to serve two competing objectives: surface inventory that is relevant to the buyer, and give sellers the visibility (views) they paid for before their auctions end. Optimizing either alone breaks the other.

## Approach / System design
The system evolved through three iterations. Iteration 1, ratio ranking: weighted random selection scored by urgency — remaining views needed divided by time left in the auction — which prioritized items in urgent need of views but ignored relevance. Iteration 2, heuristic ranking: combined the visibility signal with manually weighted relevance features such as title similarity and price similarity; A/B tests showed CTR improvements, but manual weight tuning did not scale and limited how many features could be used. Iteration 3, ML ranking with epsilon-greedy: with probability 0.95 rank by a logistic regression model's click predictions, and with probability 0.05 fall back to the ratio-based urgency score for underperforming items — optimizing the two objectives separately instead of forcing them into one formula.

## Key decisions
- Split the two objectives via epsilon-greedy (ε=0.05) rather than blending relevance and seller-visibility into a single hand-tuned score.
- Choose logistic regression over more complex models for production simplicity, with a stated plan to migrate to boosting trees as inventory grows.
- Iterate deliberately from heuristics to ML, using each stage's A/B results to justify the next.

## Stack
Logistic regression ranker with 30+ features covering recommendation quality, user preference, and seed-item similarity; trained on roughly two weeks of click-log data; epsilon-greedy serving policy with a ratio-based fallback arm.

## Results
The ML ranker showed strong uplift in buyer engagement over the heuristic baseline in A/B testing (the article does not publish exact percentages). Offline analysis tracked view distribution, coverage percentage, and CTR uplift to confirm seller-side objectives were still met.

## Takeaways
When two objectives genuinely conflict, an exploration policy that dedicates a small traffic slice to the secondary objective can be cleaner than a blended score. Starting with a simple linear model and a clear iteration path (heuristic → logistic regression → boosted trees) let eBay ship value early while keeping the door open for nonlinear feature interactions later.
