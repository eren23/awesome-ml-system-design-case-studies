---
id: cs1773
title: JD-BP: A Joint-Decision Generative Framework for Auto-Bidding and Pricing
company: JD.com
primary_category: ads
sub_category: bidding
year: 2026
source_url: https://arxiv.org/abs/2604.05845
tags: [auto-bidding, pricing, generative, return-to-go, gsp]
---

# JD-BP: A Joint-Decision Generative Framework for Auto-Bidding and Pricing
**JD.com** · 2026 · [source](https://arxiv.org/abs/2604.05845)

## Problem
Auto-bidding optimizes real-time bids for advertisers under KPI constraints such as ROI targets and budgets. In practice, model prediction errors and feedback latency push bidding strategies away from the optimal allocation, degrading efficiency — and the bid alone has no lever to correct the resulting drift in what advertisers actually pay.

## Approach / System design
JD-BP is a joint generative decision framework that outputs two things per decision: a bid value and a pricing correction term. The pricing correction is applied additively on top of the payment mechanism (e.g., GSP), giving the system a second control surface to compensate for prediction error and cumulative bias. A memory-less Return-to-Go mechanism maximizes future value while the pricing corrections absorb accumulated bias. Because no production system has historical joint bid+pricing decisions, a trajectory augmentation algorithm synthesizes joint bidding-pricing trajectories from existing base policies, making the framework plug-and-play on top of what is already deployed. Learning is refined with Energy-Based Direct Preference Optimization using cross-attention modules to coordinate the two decisions.

## Key decisions
- Treat pricing as a learnable correction jointly generated with the bid, instead of leaving the payment rule fixed and pushing all adaptation into bids.
- Use a memory-less Return-to-Go formulation, delegating cumulative-bias handling to the pricing corrections.
- Bootstrap training data via trajectory augmentation from existing base policies, avoiding a cold-start data problem and enabling plug-and-play deployment.
- Apply Energy-Based DPO with cross-attention to align the joint bid/pricing outputs.

## Stack
Generative decision model combining RL-style return-to-go conditioning with generative modeling and cross-attention; layered onto a GSP-style payment mechanism in JD.com's ad auction system; offline evaluation on the AuctionNet dataset.

## Results
State-of-the-art performance in offline evaluation on AuctionNet. In production A/B tests at JD.com, ad revenue increased 4.70% and target cost improved 6.48%.

## Takeaways
When bids alone cannot fix allocation drift caused by prediction error and delayed feedback, adding a jointly learned pricing correction gives the platform a second, complementary knob. The trajectory-augmentation trick — manufacturing joint decision data from existing single-decision policies — is what made the idea deployable without waiting for new logged data.
