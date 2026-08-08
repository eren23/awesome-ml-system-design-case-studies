---
id: cs1857
title: PayPal — Declarative Feature Engineering at PayPal
company: PayPal
primary_category: data
sub_category: feature-store
year: 2023
source_url: https://developer.paypal.com/community/blog/declarative-feature-engineering-at-paypal/
tags: [feature-engineering, declarative, feature-store, time-travel, self-service, fraud]
---

# PayPal — Declarative Feature Engineering at PayPal
**PayPal** · 2023 · [source](https://developer.paypal.com/community/blog/declarative-feature-engineering-at-paypal/)

## Problem
Data scientists at PayPal spent disproportionate time writing and debugging data pipeline code rather than focusing on feature design. Different teams duplicated feature computation logic, making it hard to reuse signals and creating inconsistencies between training and serving environments. Point-in-time correctness for historical backfills—essential for fraud detection—required careful manual implementation prone to data leakage.

## Approach / System design
PayPal built a self-service declarative feature engineering platform where data scientists specify what a feature computes rather than how it is executed. The platform parses these declarations and auto-generates optimized execution pipelines. It natively handles point-in-time time-travel semantics for historical backfills, ensuring training datasets reflect only information that was available at each event timestamp. Feature definitions are registered in a shared feature store, enabling cross-team reuse of validated features.

## Key decisions
Making time-travel a first-class platform concern rather than a responsibility of individual users was critical for preventing data leakage in fraud models. The declarative interface lowered the skill floor required to produce production-quality features, expanding the contributor pool beyond pipeline-savvy engineers.

## Stack
Not covered in the source.

## Results
Not covered in the source.

## Takeaways
Declarative feature engineering shifts the cognitive burden from pipeline implementation to feature design, which is where data scientists provide the most value. Built-in time-travel support is a force multiplier for fraud and risk use cases because it removes a common source of subtle training data leakage.
