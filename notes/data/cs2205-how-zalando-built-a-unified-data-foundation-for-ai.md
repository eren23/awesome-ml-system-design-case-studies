---
id: cs2205
title: How Zalando Built a Unified Data Foundation for AI and Analytics on Databricks
company: Zalando
primary_category: data
sub_category: data-discovery
year: 2026
source_url: https://databricks.com/blog/how-zalando-built-unified-data-foundation-ai-and-analytics-databricks
tags: [unity-catalog, databricks, metric-views, genie, semantic-layer, AI-analytics, data-foundation, data-mesh]
---

# How Zalando Built a Unified Data Foundation for AI and Analytics on Databricks
**Zalando** · 2026 · [source](https://databricks.com/blog/how-zalando-built-unified-data-foundation-ai-and-analytics-databricks)

## Problem
Zalando serves 50M+ active customers with more than 7,000 brands and partners across Europe; its microservices emit terabytes of events. Governance was strained and metrics diverged — Marketing dashboards and Finance reports showed different "Net Revenue" numbers because metric definitions lived in isolated silos across BI tools, SQL scripts, and materialized tables.

## Approach / System design
Zalando built a three-layer foundation on Databricks. Foundation layer — identity-based governance with a dual-catalog pattern: private Unity Catalog catalogs give each domain team self-service autonomy, while a shared catalog exposes company-wide data exclusively through Dynamic Views under strict central governance, with access expressed as reusable policies tied to people and groups. Semantic layer — "Metrics as Code": business logic centralized into star-schema-based Metric Views, defined in YAML, version-controlled, and deployed via GitOps with automated validation (uniqueness, naming conventions, ownership), separate dev environments, and four-eyes approval. AI layer — Genie grounded in the semantic layer answers natural-language questions; when asked about a metric like NMV, it queries the governed Metric View definition instead of computing from raw tables.

## Key decisions
- All cross-org sharing goes through Dynamic Views, enabling custom GDPR-compliant access logic and full auditability, rather than direct table grants.
- Data-sharing provisioning is GitOps-driven: PRs with config files trigger automated validation and provisioning, keeping governance from bottlenecking teams.
- Grounded the conversational AI in Metric Views rather than letting it generate SQL over raw tables — accuracy comes from governed semantics.
- Row/column-level security is inherited by Metric Views from underlying Unity Catalog tables so compliance flows through the stack.

## Stack
Databricks Unity Catalog, Dynamic Views, Metric Views, Genie (conversational analytics) and Agent Mode (root-cause analysis), GitOps with YAML metric definitions.

## Results
No quantitative outcomes are reported. Qualitatively, non-technical teams get quick answers to granular questions without SQL, and Agent Mode is projected (not yet measured) to cut preparation for performance meetings from hours to minutes.

## Takeaways
Reliable AI analytics is downstream of a governed semantic layer — LLMs give correct answers when they query pre-defined business logic, not raw tables. Separating data creation from consumption (private vs. shared catalogs) balances domain autonomy with central compliance, and GitOps makes governance scalable and auditable. Careful curation of data and context also keeps conversational-AI costs contained.
