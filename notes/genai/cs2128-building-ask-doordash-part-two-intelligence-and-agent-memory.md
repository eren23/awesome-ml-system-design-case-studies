---
id: cs2128
title: "Building Ask DoorDash Part Two: Intelligence and Agent Memory"
company: DoorDash
primary_category: genai
sub_category: agents
year: 2025
source_url: https://careersatdoordash.com/blog/building-ask-doordash-part-two-intelligence/
tags: [memory, personalization, agentic-ordering, long-term-memory, in-session-memory, conversion, dietary-preferences]
---

# Building Ask DoorDash Part Two: Intelligence and Agent Memory
**DoorDash** · 2025 · [source](https://careersatdoordash.com/blog/building-ask-doordash-part-two-intelligence/)

## Problem
Ask DoorDash's agentic ordering experience needed durable, structured understanding of user preferences, constraints, and habits across sessions. Three gaps blocked this: memory generation and agent consumption need different primitives (query planning, hybrid retrieval, ranking, prompt injection); naive top-K retrieval wastes context budget because different tasks need different memory subsets; and preferences stated in conversation evaporate after the session without explicit extraction.

## Approach / System design
A three-layer memory system feeds three complementary memory types — long-term memory generated offline from order history, in-session context (e.g., cart contents, recency-weighted), and conversational memory (explicitly stated preferences). Long-term batch pipelines produce structured blocks (dietary preferences, dining patterns, brand and store preferences) with versioned components and dense embeddings, stored in distributed SQL with vector/ANN search and namespace-partitioned multi-tenancy. Agents consume memory through a four-stage pipeline: intent/scope resolution, query planning (modality, target namespace, filter envelope), parallel retrieval with semantic ranking and recency tie-breaking, and context engineering that returns structured results with category, timestamp, and relevance score. A conversational-memory flywheel runs fire-and-forget extraction jobs after user turns, applies LLM-driven classification with domain-aware durability rules, then deduplicates and consolidates via semantic search; forgetting uses two-stage semantic search plus LLM validation to avoid over-deletion.

## Key decisions
- Moved from pre-computed static embeddings to server-side embedding at write time, so embedding-model upgrades don't require corpus reprocessing.
- "Scan before read" for large memory surfaces: expose lightweight metadata before spending tokens on full retrieval; a Memory Bank Index shows agents the available vocabulary.
- Durability rules vary by vertical — "I don't want ramen" is transient in restaurant context unless paired with always/never language, while "I prefer Oatly" is durable in grocery.
- Lifecycle by fact type: stated dietary preferences never expire; pantry staples expire on consumption/replenishment patterns.
- Aggressive exclusion of irrelevant facts — injecting too many competing facts caused the agent to drop instructions.

## Stack
Vector database with ANN search, multi-tenant distributed SQL storage with namespace partitioning, message queue for async embedding computation, LLM-based extraction/classification pipeline, and skill-based prompt management.

## Results
Early production data over a 7-day window: the grocery agent saw ~24% higher relative checkout conversion with a full memory profile, ~17% larger average baskets, ~7% fewer conversational turns, ~33% fewer intent misunderstandings, and ~24% fewer irrelevant results. The restaurant assistant saw ~15% higher relative conversion on open-ended queries and the same ~33% reduction in misunderstanding.

## Takeaways
Memory works best as shared infrastructure rather than a per-agent feature; task-aware retrieval and aggressive pruning matter more than raw recall; and extraction rules must be domain-specific or the memory fills with transient noise.
