---
id: cs1845
title: Netflix — Building and Scaling Data Lineage at Netflix
company: Netflix
primary_category: data
sub_category: data-discovery
year: 2019
source_url: https://netflixtechblog.com/building-and-scaling-data-lineage-at-netflix-to-improve-data-infrastructure-reliability-and-1a52526a7977
tags: [data-lineage, metadata, metacat, graph, data-platform]
---

# Netflix — Building and Scaling Data Lineage at Netflix
**Netflix** · 2019 · [source](https://netflixtechblog.com/building-and-scaling-data-lineage-at-netflix-to-improve-data-infrastructure-reliability-and-1a52526a7977)

## Problem
Netflix's data infrastructure spans many heterogeneous compute engines and storage systems, making it difficult to understand how data flows between them. Without end-to-end lineage, diagnosing reliability incidents, meeting SLAs, and identifying unused or costly datasets required time-consuming manual investigation.

## Approach / System design
Netflix built a pull-based lineage system that models data relationships as a directed graph. Rather than requiring producers to emit lineage events, the system scrapes existing metadata and execution logs from multiple sources—Metacat (the metadata catalog), Genie (the job orchestration service), Spark query plans, and S3 access logs—and stitches them into a unified lineage graph. This approach meant lineage coverage expanded automatically as new jobs ran without requiring code changes.

## Key decisions
Choosing a pull-based model over a push-based one eliminated the need for every team to instrument their pipelines, lowering adoption friction significantly. Modeling lineage as a graph allowed the system to support both fine-grained field-level queries and coarse-grained dataset-level queries from the same underlying structure.

## Stack
Metacat (metadata catalog), Genie (job scheduler), Apache Spark, Amazon S3, graph storage layer.

## Results
Not covered in the source.

## Takeaways
Pulling lineage from existing infrastructure artifacts rather than requiring explicit instrumentation is the most practical path to broad coverage in a heterogeneous data environment. A graph data model naturally expresses the branching and merging nature of data pipelines and supports diverse downstream use cases including reliability monitoring, cost attribution, and impact analysis.
