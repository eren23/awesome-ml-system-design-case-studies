---
id: cs2304
title: Recommending Search Filters To Improve Conversions At Airbnb
company: Airbnb
primary_category: search
sub_category: query-understanding
year: 2026
source_url: https://arxiv.org/abs/2602.23717
tags: [filter-recommendation, mlp, conversion-optimization, latency, a-b-testing, arxiv-2026]
---

# Recommending Search Filters To Improve Conversions At Airbnb
**Airbnb** · 2026 · [source](https://arxiv.org/abs/2602.23717)

## Problem
Search filters help guests narrow Airbnb's diverse inventory, but their contribution to actual bookings was underexplored: filters are an intermediate UI tool, and the link between surfacing the right filter and the lower-funnel outcome (a booking conversion) had not been directly optimized. The system also had to handle cold-start cases and meet stringent production serving requirements.

## Approach / System design
Airbnb designed and built a filter recommendation system from the ground up, framing the modeling target as booking conversion rather than filter engagement — recommending the filters most likely to lead a guest to book, not merely the ones they might click. The deployed model is an MLP-based recommender serving at sub-10ms latency (per the catalog metadata), and the framework was validated end-to-end through online A/B tests with ablation studies confirming component contributions.

## Key decisions
- Optimize for the downstream business outcome (booking conversion) instead of the proximate signal (filter usage).
- Engineer for production constraints from the start: low-latency serving and cold-start handling shaped the design.
- Prove causal impact with online A/B testing plus ablations rather than relying on offline metrics.

## Stack
MLP-based recommendation model served at sub-10ms latency (per catalog metadata); further architectural and infrastructure details are not covered in the source.

## Results
The deployed system delivered incremental booking conversion lifts validated through online A/B testing, with ablation studies confirming the results. Specific lift percentages are not stated in the source.

## Takeaways
Intermediate UX affordances like filters can be treated as ML surfaces optimized for end-funnel outcomes. Targeting conversions directly — and holding the system to production latency and cold-start requirements — turned a navigation aid into a measurable booking driver.
