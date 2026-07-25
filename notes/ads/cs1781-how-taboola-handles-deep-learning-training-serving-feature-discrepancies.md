---
id: cs1781
title: How Taboola Handles Deep Learning Training-Serving Feature Discrepancies (Sherlock)
company: Taboola
primary_category: ads
sub_category: ctr-prediction
year: 2025
source_url: https://www.taboola.com/engineering/discrepancy-solution/
tags: [training-serving-skew, monitoring, feature-quality, mlops]
---

# How Taboola Handles Deep Learning Training-Serving Feature Discrepancies (Sherlock)
**Taboola** · 2025 · [source](https://www.taboola.com/engineering/discrepancy-solution/)

## Problem
Taboola's deep-learning CTR models degrade when the feature values seen at serving time differ from the values recomputed offline for training. Discrepancies creep in from several directions: features are too large to store so they get recalculated, production suffers cache misses and database timeouts, and integration bugs silently change values between the two paths.

## Approach / System design
Sherlock is a three-stage detection pipeline. First, a sampling stage captures feature values from roughly 1 in 10,000 serving requests, storing them as Pageview objects in HDFS, with an hourly Spark job aggregating the samples. Second, a preprocess stage runs the existing training-preprocessing jobs in a special mode over the sampled Pageviews, recomputing every feature exactly as training would, and emits datasets holding each feature twice — the served value and the recalculated value. Third, a compare stage in Python/Pandas diffs served vs. recomputed values, uploads results to BigQuery, and monitors them against per-feature thresholds that fire Slack and PagerDuty alerts.

## Key decisions
- Sample at serving time rather than log everything, keeping data volume manageable while staying representative.
- Skip filtering/sampling inside Sherlock's own preprocessing so the comparison covers all captured features.
- Store each feature in dual form (served and recomputed) to enable direct side-by-side comparison.
- Give every feature configurable warning and alert threshold levels rather than one global cutoff.

## Stack
Spark, HDFS, Python, Pandas, Google BigQuery, Slack, PagerDuty.

## Results
Fixing a single discrepant feature surfaced by Sherlock lifted global RPM (Revenue Per Mille) by 1.31%. The system also stopped the team from removing genuinely valuable features that had been misdiagnosed as broken.

## Takeaways
Training-serving skew is an ongoing operational hazard, not a one-time bug: continuous, sampled comparison of served vs. recomputed features guards models against accidental feature corruption during development, and a single corrected feature can move a business-level revenue metric.
