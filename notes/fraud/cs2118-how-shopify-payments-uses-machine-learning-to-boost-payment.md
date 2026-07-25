---
id: cs2118
title: How Shopify Payments Uses Machine Learning to Boost Payment Success Rates and Cut Fraud Chargebacks
company: Shopify
primary_category: fraud
sub_category: payment-fraud
year: 2025
source_url: https://www.shopify.com/enterprise/blog/shopify-payments-pre-authorization
tags: [3ds, pre-authorization, chargeback-reduction, payment-optimization, production-ml]
---

# How Shopify Payments Uses Machine Learning to Boost Payment Success Rates and Cut Fraud Chargebacks
**Shopify** · 2025 · [source](https://www.shopify.com/enterprise/blog/shopify-payments-pre-authorization)

## Problem
Merchants have historically had to trade security against conversion: false declines cost an estimated $443 billion annually in lost legitimate sales, every $1 of fraud loss carries about $4.41 in total cost, and 18% of cart abandonments stem from complex checkout flows. Blanket authentication rules punish good customers while still letting fraud through.

## Approach / System design
Shopify trained an ML model that decides, per transaction, whether to trigger a 3D Secure (3DS) pre-authorization challenge. The model assesses risk across the whole customer journey — from landing on the site through checkout — and routes low-risk transactions through a frictionless flow while sending high-risk ones to the card issuer for a 3DS challenge. This replaces static rule-based gating with selective, risk-scored authentication.

## Key decisions
- Replace rigid Address Verification System (AVS) rules with ML-based risk assessment that still incorporates AVS and CVV signals.
- Apply 3DS selectively rather than universally, preserving conversion for low-risk buyers.
- Ship the capability platform-wide so every Shopify Payments merchant benefits without individual tuning.

## Stack
Not covered in the source beyond an ML risk model trained on Shopify's transaction data (billions of transactions per the catalog metadata) integrated with the 3DS authentication flow.

## Results
- Payment success rate up 26 basis points, translating to roughly $471 million in additional annual payment volume.
- Fraud chargebacks down 20% (8 bps off a 41 bps base), about $62 million in annual direct savings and $273 million including full chargeback costs.
- 0.33% more transactions processed versus the rigid AVS-rule regime.

## Takeaways
Selective, model-driven authentication breaks the assumed trade-off between fraud protection and conversion: the same system raised approval rates and cut chargebacks simultaneously.
