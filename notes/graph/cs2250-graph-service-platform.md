---
id: cs2250
title: Graph Service Platform
company: Grab
primary_category: graph
sub_category: gnn
year: 2023
source_url: https://engineering.grab.com/graph-service-platform
tags: [graph-infrastructure, Amazon-Neptune, Kafka, DynamoDB, fraud-detection, AML, graph-database]
---

# Graph Service Platform
**Grab** · 2023 · [source](https://engineering.grab.com/graph-service-platform)

## Problem
Grab needed to detect fraud in its mobility business by finding data linkages — for example, multiple accounts sharing physical devices to illicitly maximize earnings. Analyzing large volumes of highly interconnected data demands real-time graph search, which the existing infrastructure could not provide.

## Approach / System design
A four-layer platform-as-a-service architecture. Storage: raw CSV files in S3, graph data in Amazon Neptune, metadata in DynamoDB. Driver layer: Gremlin, Neptune, S3, and DynamoDB connectors. Service layer: cluster/instance management, schema handling, and graph algorithms. API layer: RESTful endpoints for both real-time search (OLTP) and batch analysis (OLAP). Data flows via ETL from S3 into Neptune, validated against DynamoDB-held schemas before import, while Kafka streams inject live events.

## Key decisions
- Amazon Neptune as the managed graph database for persistent relationship storage.
- Kafka streaming for online data injection (e.g. user authentication events), reducing pressure on the database.
- Asynchronous interaction between the service layer and Neptune to sustain real-time request handling.
- Separation of offline batch loading from online stream ingestion for flexibility.

## Stack
Amazon Neptune, Amazon S3, DynamoDB, Gremlin, Kafka/Confluent, RESTful APIs.

## Results
No quantitative metrics are provided in the article.

## Takeaways
Graph databases enable relationship queries directly at scale, and a platform layer that abstracts the infrastructure lets fraud/AML teams focus on schema design instead of operations. The same platform generalizes beyond fraud detection to personalized search, financial services, and risk prediction.
