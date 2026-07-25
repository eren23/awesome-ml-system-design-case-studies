---
id: cs2387
title: Building a state-of-the-art card fraud detection system in 9 months
company: Revolut
primary_category: fraud
sub_category: payment-fraud
year: 2023
source_url: https://medium.com/revolut/building-a-state-of-the-art-card-fraud-detection-system-in-9-months-96463d7f652d
tags: [card-fraud, real-time, low-latency, ml, fintech, sherlock]
---

# Building a state-of-the-art card fraud detection system in 9 months
**Revolut** · 2023 · [source](https://medium.com/revolut/building-a-state-of-the-art-card-fraud-detection-system-in-9-months-96463d7f652d)

## Problem
Revolut needed to minimize card-fraud losses (and losses from wrongly blocked transactions) without the armies of manual transaction analysts traditional banks employ. Framed as binary classification — fraudulent or not — with precision, recall, and false-positive count as the primary metrics, plus a special emphasis on catching the first transaction in a fraudulent sequence. The fraud rate in training data was around 0.03%, an extreme class imbalance.

## Approach / System design
Sherlock is a lambda architecture: a real-time scoring service paired with a nightly batch pipeline. Nightly, Cloud Composer (Airflow) orchestrates a delta dump from PostgreSQL to BigQuery; Apache Beam jobs on Dataflow generate leakage-free training data (features for each transaction computed only from that user's chronologically earlier transactions) and build user/merchant profiles stored in Couchbase; Catboost models train on Google Cloud AI Platform with artifacts in Cloud Storage. In real time, the processing backend POSTs each transaction to a Flask app on App Engine, which fetches user and merchant profiles from Couchbase, builds the same feature vector as training, scores with the pre-loaded model, and responds — all within 50 ms. Above the fraud threshold, the transaction is declined, the card frozen, and a push notification asks the user to confirm; "it's me" unblocks the card, "not me" terminates it with a free replacement. Models retrain every night on missed fraud and incorrect declines. Features span three families: raw transaction attributes (merchant, amount, time of day), user-relative deviations (speed of transaction, amount vs. that user's typical spend per merchant/category/payment method/time, first-time merchant flags), and merchant-focused aggregates (how many users transact there, fraud reports, merchant age at Revolut).

## Key decisions
- Lambda architecture: nightly batch corrects profile inaccuracies while real-time scoring stays under the 50 ms budget.
- Catboost chosen after benchmarking Vowpal Wabbit linear models, XGBoost, random forest, SVM variants, one-class SVM, and TensorFlow neural nets — it won on metrics and inference speed, handled heterogeneous numeric+categorical data, and needed little hyperparameter tuning.
- Imbalance handling: downsample non-fraud to ~10% fraud ratio, then weight fraudulent transactions by amount and other factors; validate on five chronologically future weeks at the true production fraud ratio.
- Close the loop through the user: in-app confirmation of declined transactions both automates resolution and generates labels.
- Python end to end for data science/production alignment; serverless GCP services to avoid infrastructure maintenance.

## Stack
Python, Catboost, Apache Beam on Google Cloud Dataflow, BigQuery, PostgreSQL, Cloud Composer (Airflow), Google Cloud AI Platform, Cloud Storage, Couchbase (in-memory profile store), Flask on App Engine, Stackdriver and Kibana for monitoring.

## Results
- 96% of fraudulent transactions caught; 30% of fraud predictions are true positives.
- Over $3M saved in the first year in production; fraud losses at about 1 cent per $100 of volume.
- End-to-end transaction scoring within 50 ms, with nightly retraining keeping models current.

## Takeaways
- Having the right data matters more than the algorithm — the project started with plumbing PostgreSQL into BigQuery, not with model selection.
- Preventing data leakage via chronological feature construction, and validating at production fraud ratios, is what makes offline metrics predictive of live performance.
- Gradient boosting on decision trees (Catboost) remains a strong default for heterogeneous tabular fraud data under tight latency budgets.
- A small team can ship a mission-critical ML system in nine months by leaning on managed/serverless infrastructure and closing the label loop through the product itself.
