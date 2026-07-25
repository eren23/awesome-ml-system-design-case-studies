---
id: cs2385
title: How Data Science and Applied Science Work Together at Wolt
company: Wolt
primary_category: forecast
sub_category: eta-prediction
year: 2025
source_url: https://careers.wolt.com/en/blog/tech/inside-data-science-applied-science-wolt
tags: [eta-prediction, delivery-time, ml-production, applied-science, food-delivery]
---

# How Data Science and Applied Science Work Together at Wolt
**Wolt** · 2025 · [source](https://careers.wolt.com/en/blog/tech/inside-data-science-applied-science-wolt)

## Problem
Wolt runs delivery operations across 30+ countries and needs both rigorous decision-making (experimentation, causal analysis) and intelligent real-time systems (ETA prediction, courier assignment). The article addresses how to organize two distinct disciplines so analytics and production ML reinforce each other rather than overlap.

## Approach / System design
Two complementary functions: Data Science sits in the Analytics org and drives decisions through experimentation and causal inference; Applied Science sits in the Engineering org and ships production ML and optimization algorithms. Both are embedded in domain areas (e.g., Courier, Merchant) and collaborate with Product, Engineering, and Operations. Applied Science powers courier-assignment optimization, real-time delivery-time prediction, personalization that accounts for user intent and location, and demand forecasting for automated inventory management — all built on an internal ML Platform. The Estimated Delivery Time (EDT) work is the flagship example of the two teams collaborating on one problem.

## Key decisions
- Split "science for decisions" (Data Science / Analytics) from "science in the product" (Applied Science / Engineering) instead of one generalist role.
- Embed both roles in business domains rather than a central lab, keeping them close to Product and Operations.
- Require production-level code from Applied Science, backed by a shared internal ML Platform.

## Stack
Data Science: SQL, Python, statistical libraries, visualization tools. Applied Science: ML frameworks, optimization algorithms, and Wolt's internal ML Platform for production deployment.

## Results
- Delivery-time models generate over 57 billion delivery time estimates daily.
- The EDT collaboration produced more accurate ETAs, fewer support tickets, and better alignment between the promised and actual delivery time.

## Takeaways
- Separating decision science from production ML clarifies ownership: one makes the org smarter, the other makes the product smarter.
- Embedding scientists in domains with shared platform tooling scales ML across many surfaces (assignment, ETA, personalization, forecasting).
- ETA accuracy is a customer-experience lever — better estimates directly cut support load.
