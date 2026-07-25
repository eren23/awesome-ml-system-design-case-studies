---
id: cs2191
title: Combining Machine Learning and Homomorphic Encryption in the Apple Ecosystem
company: Apple
primary_category: cv
sub_category: object-detection
year: 2024
source_url: https://machinelearning.apple.com/research/homomorphic-encryption
tags: [homomorphic-encryption, visual-search, on-device-ml, privacy, differential-privacy, landmark-detection, nearest-neighbor-search, vector-embeddings]
---

# Combining Machine Learning and Homomorphic Encryption in the Apple Ecosystem
**Apple** · 2024 · [source](https://machinelearning.apple.com/research/homomorphic-encryption)

## Problem
On-device ML experiences often need server-side knowledge — e.g., identifying landmarks in a photo requires a global landmark database too large to ship to devices — but querying a server normally reveals user photos or queries. Apple wanted server-assisted visual search that keeps queries and results fully private.

## Approach / System design
Enhanced Visual Search in Photos combines three pieces. Homomorphic encryption (the Brakerski-Fan-Vercauteren scheme, with post-quantum 128-bit security) lets the server compute on encrypted data without ever decrypting it. Private Nearest Neighbor Search (PNNS) lets the client find approximate matches against a server-side vector database of landmark embeddings while the query stays encrypted end-to-end. On device, an ML model detects landmark regions of interest in a photo, computes an embedding, quantizes it to 8 bits, encrypts it, and sends it; the server evaluates encrypted similarity scores against the relevant database shard, merges multiple encrypted scores into a single ciphertext, and returns it; the client decrypts and a lightweight multimodal reranking model finalizes the match.

## Key decisions
- 8-bit quantization of embeddings to shrink request size and server compute at scale.
- Sharding the landmark database into disjoint clusters, with clients selecting the relevant shard locally via a precomputed codebook so the server never learns the exact query region.
- Anonymization by an OHTTP relay run by a third party to hide IP addresses, plus differential privacy — fake queries mixed with real ones with parameters ε = 0.8, δ = 10⁻⁶.
- Merging encrypted similarity scores into one ciphertext to keep responses compact.

## Stack
BFV homomorphic encryption (open-sourced as swift-homomorphic-encryption), on-device region-of-interest detection model, vector embeddings with inverted-index landmark database, PNNS protocol, OHTTP relay, lightweight multimodal reranker.

## Results
No quantitative performance metrics are given in the source; the deployed outcome is production visual landmark search in Photos where Apple's servers never see user images, queries, or results.

## Takeaways
HE plus PNNS plus differential privacy makes "server-enriched on-device ML" viable in production: the engineering levers that make it affordable are aggressive embedding quantization, database sharding with client-side shard selection, and compact encrypted responses.
