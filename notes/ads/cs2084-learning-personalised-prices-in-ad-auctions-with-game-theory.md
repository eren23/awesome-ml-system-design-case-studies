---
id: cs2084
title: Learning Personalised Prices in Ad Auctions with Game Theory and Deep Learning
company: Spotify
primary_category: ads
sub_category: auction
year: 2025
source_url: https://research.atspotify.com/2025/11/learning-personalised-prices-in-ad-auctions-with-game-theory-and-deep
tags: [personalized-pricing, game-theory, deep-learning, reservation-price, auction-mechanism, revenue-optimization]
---

# Learning Personalised Prices in Ad Auctions with Game Theory and Deep Learning
**Spotify** · 2025 · [source](https://research.atspotify.com/2025/11/learning-personalised-prices-in-ad-auctions-with-game-theory-and-deep)

## Problem
Spotify needed to set optimal reservation (minimum) prices for impression-based (CPM) ad auctions. Advertisers' true valuations are hidden — only their bids are observable, and bids are strategic. Standard reserve-price methods built for cost-per-click auctions don't transfer well to CPM settings.

## Approach / System design
The team combined auction theory with deep learning: (1) derive the symmetric Nash equilibrium bidding relationships for generalized second-price auctions in a CPM setting; (2) train a Mixture Density Network to predict the full distribution of advertiser values (not point estimates), conditioned on user features (age, location, market) and advertiser characteristics; (3) embed the Nash equilibrium condition directly into the network's loss function, so the learned latent value distributions are those that would rationally generate the observed bids; (4) estimate equilibrium revenue under candidate reservation prices via Monte Carlo simulation; (5) find revenue-maximizing personalized reserves with gradient-based optimization.

## Key decisions
- Invert observed bids into latent value distributions through the equilibrium constraint, rather than treating bids as values.
- Predict full value distributions (MDN) instead of point estimates, enabling revenue simulation under counterfactual reserves.
- Personalize reserve prices on both user and advertiser features rather than setting market-wide reserves.

## Stack
Mixture Density Network with a game-theoretic (Nash equilibrium) constraint in the loss, Monte Carlo revenue simulation, gradient-based price optimization. Presented at NeurIPS 2025.

## Results
Evaluated on 100,000 real Spotify auctions across ten international markets: +4% average auction revenue, up to +11.8% in some markets, beating zero reserves, Myerson prices, empirical maximization, and sampling-based baselines. Gains varied with market competitiveness and advertiser preference heterogeneity.

## Takeaways
Embedding economic equilibrium structure into a neural network yields pricing policies that are both effective and explainable: the model learns what advertisers must value for their bids to be rational, which is the correct foundation for setting reserves — an approach the authors argue generalizes beyond ad auctions.
