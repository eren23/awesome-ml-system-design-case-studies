---
id: cs2144
title: Why Plaid Built the Transaction Enrichment Engine
company: Plaid
primary_category: nlp
sub_category: entity-resolution
year: 2023
source_url: https://plaid.com/blog/transaction-enrichment-engine/
tags: [transaction-enrichment, merchant-name-parsing, location-parsing, bert, named-entity-recognition, fintech, production]
---

# Why Plaid Built the Transaction Enrichment Engine
**Plaid** · 2023 · [source](https://plaid.com/blog/transaction-enrichment-engine/)

## Problem
Raw bank transaction descriptions are jumbled strings of letters and numbers. Banks and fintech apps need those strings turned into accurate, actionable data — who the merchant is, where the purchase happened, what category it belongs to — at a scale of hundreds of millions of transactions per day.

## Approach / System design
A multi-layered pipeline processing 500M+ transactions daily:
1. **Pre-processing:** subword-based tokenization normalizes messy description strings.
2. **Named Entity Recognition:** extracts merchant names, locations, and store numbers.
3. **Named Entity Linking:** maps extracted entities to records in an internal knowledge base, with a multi-attribute candidate-ranking engine to cover long-tail merchants.
4. **Enrichment insights:** derives categorization and additional signals on top of the linked entities.

## Key decisions
- Hybrid design: regex and fuzzy matching handle templated and slightly corrupted formats, while a Transformer-based language model generalizes to unseen patterns — balancing accuracy, coverage, and interpretability.
- Built an internal knowledge base so enrichment draws on structured merchant metadata, not just the raw text.
- Consolidated a legacy taxonomy of 600+ categories down to 16 primary and 104 sub-categories.

## Stack
Regex pattern matching, fuzzy string matching, a Transformer-based (BERT-like) language model for NER, fully-connected neural layers for multi-class categorization, internal knowledge base with candidate ranking.

## Results
- 90%+ merchant coverage at 99% precision.
- 90%+ accuracy on Personal Finance Category assignment.
- 500M+ transactions processed daily.

## Takeaways
- Layered heuristics-plus-ML systems beat any single technique on messy real-world text.
- A curated knowledge base is what turns entity extraction into genuinely useful enrichment.
- Simplifying the category taxonomy (600+ → 120) was itself a product decision that improved usability.
