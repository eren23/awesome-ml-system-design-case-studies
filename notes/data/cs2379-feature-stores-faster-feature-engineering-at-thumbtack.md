---
id: cs2379
title: Feature Stores & Faster Feature Engineering at Thumbtack
company: Thumbtack
primary_category: data
sub_category: feature-store
year: 2022
source_url: https://medium.com/thumbtack-engineering/feature-stores-faster-feature-engineering-506e74811c56
tags: [feature-store, bigquery, dynamodb, search-ranking, ml-infrastructure]
---

# Feature Stores & Faster Feature Engineering at Thumbtack
**Thumbtack** · 2022 · [source](https://medium.com/thumbtack-engineering/feature-stores-faster-feature-engineering-506e74811c56)

## Problem
Thumbtack's search ranking models train on features logged in search events. Any new feature had to be implemented in production, logged, and left to accumulate for weeks or months before there was enough training data — a painfully slow iteration cycle. An interim fix (simulating new features from historical data offline) introduced a second problem: feature distributions diverged between offline training (SQL) and online ranking (Spark jobs writing to DynamoDB), and there was no way to tell whether a search was served with today's or yesterday's feature data.

## Approach / System design
After studying existing feature stores (Uber's Palette with Hive/Cassandra dual stores, Airbnb's Zipline declarative framework), Thumbtack built only the subset it needed. The nightly Spark jobs were restructured around a daily BigQuery snapshot of feature data derived from events data ("Offline Features"). Model training reads from this snapshot; a Spark job copies the same snapshot into DynamoDB for online serving — so offline and online distributions are identical by construction. A version field (the aggregation date) is attached to feature data in DynamoDB and logged in search events, resolving the "which day's data served this search" ambiguity. New features are created by backfilling the historical snapshots, and training data picks them up immediately. Additionally, all columns of the Offline Features table are stored in a schema-less key-value field in DynamoDB, so adding a new feature (column) needs no Spark job changes and can be done through the existing BigQuery SQL events pipeline.

## Key decisions
- Build the minimal feature-store subset (backfillable offline features + synchronized online copy) instead of adopting a full platform like Feast up front.
- Populate the online store from the same offline snapshot used for training, making online/offline consistency structural rather than something to reconcile.
- Version feature data by aggregation date and log it in events for exact reproducibility.
- Schema-less key-value storage in DynamoDB to democratize feature creation for engineers/data scientists not fluent in Spark.
- Consciously accept that features not reconstructible from events data (e.g., a pro's settings or full text profile) are unsupported for now, since they are a minority.

## Stack
BigQuery (offline feature snapshots, SQL events pipeline), Spark (nightly aggregation and sync jobs), DynamoDB (online store with schema-less key-value field), search ranking service consuming features at serve time.

## Results
New ranking features (e.g., customer engagement on professional profiles, search filter selections) could be backfilled from historical events and trained on immediately instead of waiting weeks or months for logs to accumulate. Feature-logic bugs stopped being velocity killers — fix the logic, re-backfill, retrain. Growing use also exposed limits: the filter-selection experiment hit DynamoDB read-capacity thresholds and raised serving-latency concerns, showing the online side must now catch up with what offline enables.

## Takeaways
- Backfillable features from events data collapse ML iteration time from months to days.
- Deriving the online store from the training snapshot is the cleanest way to kill offline/online skew.
- Building only the feature-store functionality you actually need is a viable path — with open-source options like Feast as the fallback when needs outgrow it.
