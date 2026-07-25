---
id: cs2122
title: Mastercard Accelerates Card Fraud Detection with Generative AI Technology
company: Mastercard
primary_category: fraud
sub_category: payment-fraud
year: 2024
source_url: https://newsroom.mastercard.com/news/press/2024/may/mastercard-accelerates-card-fraud-detection-with-generative-ai-technology/
tags: [generative-ai, large-tabular-model, compromised-card-detection, real-time, global-deployment]
---

# Mastercard Accelerates Card Fraud Detection with Generative AI Technology
**Mastercard** · 2024 · [source](https://newsroom.mastercard.com/news/press/2024/may/mastercard-accelerates-card-fraud-detection-with-generative-ai-technology/)

## Problem
Fraudsters harvest payment card numbers through malware and skimming, then sell partial card details on illegal marketplaces. Banks struggled to identify which cards were compromised — and to block them — quickly enough to prevent downstream fraud.

## Approach / System design
Mastercard deployed generative AI-based predictive technology that scans transaction data across billions of cards and millions of merchants. By analyzing transaction patterns, the system predicts the full details of compromised cards from the partial numbers appearing on illegal sites, letting issuing banks block cards faster. It also accelerates identification of merchants that are at risk or already compromised.

## Key decisions
- Apply generative modeling to transaction data for prediction of compromised card details, rather than relying on reactive fraud reporting.
- Integrate the capability into Mastercard's existing Cyber Secure solution (launched 2020), which already profiles cybersecurity posture for banks and merchants, instead of shipping a standalone product.

## Stack
Generative AI over large-scale transaction data within the Cyber Secure platform; specific model and infrastructure details are not covered in the source.

## Results
As reported by Mastercard: doubled the detection rate of compromised cards, reduced false positives by up to 200%, and increased the speed of identifying at-risk merchants by 300%.

## Takeaways
Generative AI shifts card fraud defense from reactive response to predictive mitigation — inferring what has been compromised before it is fully exploited. Automating pattern recognition across a network-scale dataset shortens the identification-to-blocking cycle, which is where fraud losses actually accrue.
