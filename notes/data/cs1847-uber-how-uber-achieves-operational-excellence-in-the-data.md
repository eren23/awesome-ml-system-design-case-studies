---
id: cs1847
title: Uber — How Uber Achieves Operational Excellence in the Data Quality Experience
company: Uber
primary_category: data
sub_category: data-quality
year: 2021
source_url: https://www.uber.com/us/en/blog/operational-excellence-data-quality/
tags: [data-quality, monitoring, test-generation, alerting, data-platform]
---

# Uber — How Uber Achieves Operational Excellence in the Data Quality Experience
**Uber** · 2021 · [source](https://www.uber.com/us/en/blog/operational-excellence-data-quality/)

## Problem
Uber operates thousands of critical datasets that feed real-time and batch ML models, financial reporting, and operational dashboards. Data quality incidents—late arrivals, schema drifts, unexpected nulls, out-of-range values—propagated silently across downstream consumers before being detected, causing cascading failures. A fragmented set of one-off monitoring scripts offered inconsistent coverage and no unified incident-response workflow.

## Approach / System design
Uber built UDQ (Uber Data Quality), a consolidated platform with three core components: a test generator that suggests quality checks from data profiling and schema analysis, an execution engine that runs approximately 100,000 tests daily across more than 2,000 critical datasets, and alert and incident managers that triage failures, route to owners, and track resolution. The system integrates with Uber's existing data catalog and pipeline orchestration, making it possible to attach quality gates to pipeline definitions.

## Key decisions
Auto-generating test suggestions from data profiling lowered the barrier for teams to adopt quality checks without requiring deep manual specification work. Consolidating alerts and incident management into a single workflow rather than routing through separate on-call systems reduced the time from detection to resolution.

## Stack
Not covered in the source.

## Results
UDQ runs approximately 100,000 daily tests over more than 2,000 critical datasets and catches roughly 90% of data quality incidents.

## Takeaways
A platform that auto-generates quality tests dramatically improves coverage because manual test authoring rarely keeps pace with schema evolution. Treating data quality as an operational discipline with its own incident lifecycle—not just a batch of monitoring alerts—creates accountability and measurable resolution SLAs.
