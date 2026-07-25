---
id: cs2386
title: "Built with BigQuery: How Sift Delivers Fraud Detection Workflow Backtesting at Scale"
company: Sift
primary_category: fraud
sub_category: payment-fraud
year: 2023
source_url: https://cloud.google.com/blog/products/data-analytics/how-sift-delivers-fraud-detection-workflow-backtesting-at-scale
tags: [bigquery, backtesting, fraud-workflow, real-time, gcp, no-code]
---

# Built with BigQuery: How Sift Delivers Fraud Detection Workflow Backtesting at Scale
**Sift** · 2023 · [source](https://cloud.google.com/blog/products/data-analytics/how-sift-delivers-fraud-detection-workflow-backtesting-at-scale)

## Problem
Sift customers process tens of millions of events daily through fraud-detection workflows. Changing a workflow (thresholds, rules, routing) in production is risky: a bad change can raise fraud cost, insult legitimate users, or hurt MAU and customer lifetime value. Merchants needed a way to simulate proposed workflow changes against historical traffic before promoting them.

## Approach / System design
Ingestion: workflow requests arrive via Cloud Pub/Sub, a Dataflow job parses the complex nested requests into a flattened, spreadsheet-like structure, and the BigQuery Storage Write API lands them in BigQuery. The data model is schema-agnostic: instead of a workflow-specific layout, records are grouped by data type, with an associative metadata (fact) table linking to data-type (dimension) tables — supporting 10,000+ custom fields per customer and letting attribute changes be declarative metadata edits rather than schema migrations. Backtesting is orchestrated by a Spring Cloud web app exposing an async API that runs three or more interdependent SQL queries in strict order, writes status records to a log table, and returns results via polling.

## Key decisions
- BigQuery (Dremel engine + Colossus columnar storage) chosen after benchmarking against alternatives for scan-heavy analytical queries.
- Schema-agnostic fact/dimension design so frequent attribute additions/removals never require schema changes.
- Async orchestration with status polling rather than synchronous request/response, given multi-query jobs.
- Capacity planned with load testing (JMeter) plus BigQuery's Slot Estimator: modeled P90/P95 latencies and what-if scenarios (±100 slots), settling on 3,000 slots.

## Stack
BigQuery (Storage Write API, Dremel, Slot Estimator), Cloud Pub/Sub, Dataflow, Spring Cloud (orchestration service), JMeter (load testing).

## Results
- Backtests over 45 days of history on terabyte-scale tables with billions of records return in ~60 seconds on average, ~2 minutes worst case for complex requests.
- Sustained 30 requests/minute in a 30-minute load test with 3,000 BigQuery slots.
- Customers can validate fraud-policy changes against real traffic before production, reducing payment friction while protecting core KPIs. (The article cites customers processing tens of millions of events per day.)

## Takeaways
- A schema-agnostic data model is what makes no-code backtesting feasible when every customer defines thousands of custom fields.
- Serverless building blocks (Pub/Sub, Dataflow, BigQuery) push scale problems to the platform and keep operational overhead low.
- Load testing plus slot-level capacity modeling turns warehouse cost/latency into a designed quantity rather than a surprise.
