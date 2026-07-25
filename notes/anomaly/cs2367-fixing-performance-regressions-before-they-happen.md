---
id: cs2367
title: Fixing Performance Regressions Before they Happen
company: Netflix
primary_category: anomaly
sub_category: outlier-detection
year: 2022
source_url: https://netflixtechblog.com/fixing-performance-regressions-before-they-happen-eab2602b86fe
tags: [changepoint-detection, anomaly-detection, performance-monitoring, regression-detection, pre-release]
---

# Fixing Performance Regressions Before they Happen
**Netflix** · 2022 · [source](https://netflixtechblog.com/fixing-performance-regressions-before-they-happen-eab2602b86fe)

## Problem
Netflix serves 222 million members on 1700+ device types; TV devices are memory constrained, so both responsiveness and memory regressions can degrade the experience or crash the app. Canary releases catch some regressions but their user base is small and reverts are messy, so the TVUI team wanted to catch regressions per commit, before merge. Pre-production performance data is scarce, only approximates real usage, and is noisy (device CPU variance, GC, network, backend activity). Their first attempt — static memory thresholds per test — required manual per-test tuning (only ~30% of test variations got thresholds), ignored context, was dominated by background noise near the threshold, and needed constant post-alert adjustment.

## Approach / System design
~50 focused performance tests each simulate a slice of member engagement (startup, profile switching, scrolling, playback, etc.), run across device/SDK combinations ("test variations"), twice per PR (on submit and on merge). Memory tests report the max observed value; responsiveness tests report the median. Validation replaced static thresholds with a two-pronged statistical approach:
- **Anomaly detection**: a data point more than n standard deviations above the recent mean (n=4, computed over the previous m=40 runs) fails the test and alerts. Thresholds are dynamic and self-adjust to background variance.
- **Changepoint detection**: e-divisive analysis (Python implementation) over the 100 most recent runs finds boundaries between distinct data distributions. Upward changepoints are treated as warnings, not failures — best for catching subtle regressions already merged but not shipped.
Each test runs 3 times regardless of outcome; the minimum of the 3 runs is used, since outliers skew high — this beat both mean and median at eliminating device noise.

## Key decisions
- Give equal weight to all runs (remove failure bias) and assess builds relative to previous builds rather than in isolation.
- Make validation automatic for every test with no pre-hoc research or manual threshold entry, applicable to any non-boolean metric.
- Fail-and-alert only on anomalies; treat changepoints as softer signals warranting investigation before release.
- Summarize 3 runs by their minimum value after mean and median both produced excess false positives.

## Stack
Python-based e-divisive changepoint detection; Netflix's TVUI test infrastructure on physical and virtual devices. The techniques are framework independent — inputs are just a current value and an array of recent values.

## Results
- Comparing March 2021 (static thresholds) with October 2021 (anomaly detection): despite far more validating test runs in October, alerts dropped to about 10% of the earlier volume, and alerts were much likelier to be genuine regressions.
- Subsequent innocuous builds inheriting a regression no longer alert (the regression raises mean and stddev, putting later builds under the threshold), unlike static thresholds which alerted every build until revert.
- PR performance checks went from almost constantly red to mostly green, with red now signaling real regressions with high confidence.
- Per-build anomaly/changepoint counts give a quick visual snapshot of problematic builds.

## Takeaways
Dynamic, data-derived thresholds beat static ones for noisy pre-production metrics: they self-calibrate to variance, need no manual upkeep, and drastically improve signal-to-noise. Pairing immediate anomaly alerts with retroactive changepoint warnings covers both sharp and subtle regressions. The approach is being extended to other repos (TV Player) and generalizes beyond performance — e.g., monitoring test-suite reliability — since it only needs a value plus its recent history.
