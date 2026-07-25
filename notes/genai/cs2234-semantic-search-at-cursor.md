---
id: cs2234
title: Semantic Search at Cursor
company: Cursor
primary_category: genai
sub_category: eval
year: 2025
source_url: https://www.cursor.com/blog/semsearch
tags: [semantic-search, code-search, embeddings, rag, codebase-indexing]
---

# Semantic Search at Cursor
**Cursor** · 2025 · [source](https://www.cursor.com/blog/semsearch)

## Problem
Coding agents need to understand and navigate large codebases to answer questions accurately. Plain grep/regex search is insufficient for conceptual queries like "where do we handle authentication?"

## Approach / System design
Cursor pairs semantic search with grep in a hybrid strategy. The semantic component is a custom in-house embedding model that indexes code segments and retrieves matches for natural-language queries. To train it, the team mines agent session traces to identify what information should have been retrieved earlier, then feeds that into an LLM ranking process that produces the training signal for the embedding model — i.e., the retriever learns from real agent behavior rather than generic code-similarity heuristics.

## Key decisions
- Combine semantic search and grep rather than relying on either alone.
- Train the embedding model on actual agent behavior (session traces) instead of generic similarity.
- Use an LLM ranker over trace-derived examples to generate relevance labels for training.

## Stack
Custom in-house embedding model; grep; an LLM ranking system for relevance scoring; the Cursor Context Bench evaluation dataset; the Cursor Composer model as the consuming agent.

## Results
12.5% average accuracy improvement (range 6.5%–23.5% depending on model); +0.3% code retention overall and +2.6% for large codebases (1,000+ files); 2.2% fewer dissatisfied follow-up requests when semantic search is available.

## Takeaways
Semantic search is currently necessary for the best results, especially in large codebases. Complementary retrieval methods beat any single approach, and learning the retriever from real agent behavior outperforms generic similarity metrics.
