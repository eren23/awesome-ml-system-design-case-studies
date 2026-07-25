---
id: cs2333
title: How we migrated a live routing system using AI-assisted refactoring
company: Datadog
primary_category: genai
sub_category: prompt-eng
year: 2026
source_url: https://www.datadoghq.com/blog/engineering/ai-assisted-storage-migration/
tags: [code-refactoring, migration, llm, ai-assisted-development, storage-migration, copilot]
---

# How we migrated a live routing system using AI-assisted refactoring
**Datadog** · 2026 · [source](https://www.datadoghq.com/blog/engineering/ai-assisted-storage-migration/)

## Problem
Stream Router, the control plane that decides how Datadog's metrics pipeline distributes hundreds of trillions of events daily, had outgrown its FoundationDB key-value data model. Critical operations exceeded transaction size limits, and the heaviest operations were estimated at 45 minutes due to thousands of sequential database round trips. Because the system is the source of truth for routing, any migration carried extreme risk.

## Approach / System design
The team redesigned the data model from key-value to relational and executed the migration in three phases with heavy LLM assistance. Phase 1 built a semantic map of the existing codebase via AI-assisted documentation focused on intent, not implementation. Phase 2 refactored method by method in a test-driven loop: stub the implementation, run end-to-end tests, feed failing output plus schema context to the model, iterate until green. Phase 3 validated in production with a blue/green setup — the new system ran alongside the old for weeks while a validator service compared responses against live traffic every 30 seconds. The new implementation slotted behind an existing Controller abstraction, isolating the change from the rest of the system.

## Key decisions
- PostgreSQL for the write path (native relational semantics and transactions), replacing FoundationDB.
- DuckDB for the read path as an embeddable snapshot server, replacing RocksDB — chosen for native array support and PostgreSQL SQL compatibility, which let write and read paths share query logic.
- Narrow, method-level prompts with specific failing tests instead of broad refactoring requests.
- Humans kept optimization work: models produced correct but sub-optimal SQL; engineers handled batching, UNNEST patterns, and query planning.
- Weeks of blue/green comparison against live data as the final correctness gate.

## Stack
PostgreSQL, DuckDB, FoundationDB (legacy), RocksDB (legacy), Claude and Cursor for AI-assisted code generation, gRPC services, blue/green deployment with an automated validator service.

## Results
Operations previously estimated at 45 minutes complete in about one second. The routing dataset shrank 40x in PostgreSQL, latencies dropped by one or more orders of magnitude (hundreds of milliseconds to a few), CPU and memory use fell across pods, and database costs dropped by 90%. Timeline: 4 weeks to proof of concept, 3 months from design to production.

## Takeaways
- Test suite quality is the ceiling on how much AI-generated code you can trust; end-to-end tests gave objective pass/fail criteria.
- Narrow prompts with concrete failing tests outperform broad context.
- LLMs excel at iteration, not optimization — human expertise still owns performance work.
- Documentation explaining why code exists pays off when models need to understand intent.
- Production blue/green validation, not theoretical correctness, closed the confidence gap.
