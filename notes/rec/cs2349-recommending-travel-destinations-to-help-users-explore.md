---
id: cs2349
title: Recommending travel destinations to help users explore
company: Airbnb
primary_category: rec
sub_category: multi-task
year: 2026
source_url: https://medium.com/airbnb-engineering/recommending-travel-destinations-to-help-users-explore-5fa7a81654fb
tags: [destination-recommendation, multi-task-learning, sequential-modeling, travel, email-personalization, user-behavior-sequences]
---

# Recommending travel destinations to help users explore
**Airbnb** · 2026 · [source](https://medium.com/airbnb-engineering/recommending-travel-destinations-to-help-users-explore-5fa7a81654fb)

## Problem
Many Airbnb users start searching without a fixed destination in mind, or abandon a search before booking. Airbnb wanted a model that could recommend travel destinations to spark inspiration, help undecided users narrow down choices, and re-engage users who walked away mid-search.

## Approach / System design
Airbnb built a destination recommendation model that consumes multiple sequences of user actions (bookings, listing views, search history) and predicts likely travel destinations. The network ends in multiple prediction heads, one per task: it is trained jointly to predict both region-level and city-level destinations. Encouraging consistency between the region and city predictions pushes the model to learn richer geolocation representations of cities. The model powers two product surfaces: destination autosuggest when a user clicks the search bar, and follow-up "abandoned search" emails that feature listings from destinations the model predicts for that user.

## Key decisions
- Multi-task learning with separate heads for region-level and city-level destination prediction, rather than a single flat destination classifier.
- Enforcing consistency between the region and city tasks so the model learns a geographic hierarchy.
- Modeling several distinct user behavior sequences (booking, view, search) instead of a single interaction stream.
- Reusing one model across two surfaces: search-bar autosuggest and post-abandonment email personalization.

## Stack
Not covered in the source.

## Results
Online A/B testing of the autosuggest integration showed significant booking gains, particularly in regions where English is not the primary language, helping both users who had not yet chosen a destination and users open to more affordable listings in neighboring cities. The abandoned-search emails featuring model-recommended destinations helped drive users back to complete bookings.

## Takeaways
Destination choice is hierarchical, and modeling it that way (region + city as joint tasks) yields better representations than treating destinations as flat labels. A single well-built recommendation model can serve multiple engagement surfaces — in-product autosuggest and lifecycle emails — and exploration-oriented recommendations can unlock bookings from users who would otherwise leave without deciding.
