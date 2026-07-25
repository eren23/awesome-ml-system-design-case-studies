---
id: cs1784
title: Conversion-Based Dynamic Creative Optimization in Native Advertising
company: Yahoo
primary_category: ads
sub_category: ctr-prediction
year: 2022
source_url: https://www.yahooinc.com/research/publications/conversion-based-dynamic-creative--optimization-in-native-advertising
tags: [dynamic-creative-optimization, cvr-prediction, offset, gemini]
---

# Conversion-Based Dynamic Creative Optimization in Native Advertising
**Yahoo** · 2022 · [source](https://www.yahooinc.com/research/publications/conversion-based-dynamic-creative--optimization-in-native-advertising)

## Problem
Yahoo's Gemini native ads marketplace historically optimized for clicks, but advertisers increasingly ran conversion-based campaigns and wanted dynamic creative optimization (DCO) — ads composed of multiple interchangeable assets — to be optimized for conversions rather than CTR.

## Approach / System design
The team built a post-auction DCO solution on top of OFFSET, Yahoo's feature-enhanced collaborative-filtering event-prediction algorithm. Auxiliary OFFSET-based models trained for combination-level CVR prediction score the possible creative-asset combinations of a winning DCO ad; those predicted CVRs are turned into a weighted distribution used to pick which combination to render at serving time, giving an explore-exploit behavior rather than always serving the argmax.

## Key decisions
- Optimize on predicted CVR instead of raw observed conversions, sidestepping conversion data sparsity and reporting delays.
- Operate post-auction — choose the creative combination after the ad wins — rather than changing the auction itself.
- Train dedicated auxiliary models for combination-level CVR rather than reusing the main event-prediction model directly.
- Serve combinations from a weighted distribution to balance exploration with exploitation.

## Stack
OFFSET, Yahoo's collaborative-filtering-based event-prediction algorithm, within the Gemini native serving system.

## Results
Fully deployed on all Gemini native traffic — billions of daily impressions across hundreds of millions of unique users, in a marketplace with yearly revenue of many hundreds of millions of dollars. The conversion-based DCO achieved a 53.5% CVR lift versus control buckets that served combinations uniformly at random.

## Takeaways
A lightweight, prediction-driven approach that respects real-world constraints — sparse and delayed conversion signals, an auction you can't touch — can still deliver a very large conversion lift; predicted rates are a workable stand-in when actual outcome data is too sparse to optimize on directly.
