---
id: cs2317
title: "Smart Fast Finish: Preventing Overdelivery via Daily Budget Pacing at DoorDash"
company: DoorDash
primary_category: ads
sub_category: budget-pacing
year: 2025
source_url: https://arxiv.org/abs/2509.07929
tags: [budget-pacing, ad-delivery, overdelivery, pacing-algorithm, attribution, sponsored-listings]
---

# Smart Fast Finish: Preventing Overdelivery via Daily Budget Pacing at DoorDash
**DoorDash** · 2025 · [source](https://arxiv.org/abs/2509.07929)

## Problem
Ad budget pacing must avoid overdelivery — burning through an advertiser's daily budget too fast and exhausting it before the intended window ends. DoorDash's sponsored-listings platform used a conventional "Fast Finish" (FF) mechanism that rapidly depletes the remaining budget near the end of the day, but its fixed parameters made it non-adaptive and left overdelivery risk unaddressed.

## Approach / System design
Smart Fast Finish (SFF) extends the standard FF feature with dynamic parameter adjustment. Instead of fixed settings, SFF continuously updates pacing parameters — notably the FF start time and the throttle rate — based on each campaign's historical delivery data, making end-of-day budget depletion adaptive per campaign.

## Key decisions
- Adapt existing FF machinery rather than replace it: keep the fast-finish pattern but learn its parameters from historical ad-campaign data.
- Calibrate per campaign using historical delivery signals so pacing responds to real spend patterns rather than static configuration.
- Validate through both online budget-split experimentation in production and offline simulation before/alongside rollout.

## Stack
Deployed as part of DoorDash's production ad budget-pacing system for sponsored listings. The abstract does not detail specific infrastructure components; the method centers on historical-data-driven parameter calibration and dynamic throttling.

## Results
SFF is in full production at DoorDash. Effectiveness was demonstrated via an online budget-split experiment and offline simulation analysis; the abstract does not disclose specific numeric metrics.

## Takeaways
Production pacing systems benefit from replacing static configuration with parameters learned from historical campaign behavior. A modest, adaptive extension of an existing mechanism (Fast Finish) can be a robust mitigation for overdelivery without redesigning the whole pacing stack.
