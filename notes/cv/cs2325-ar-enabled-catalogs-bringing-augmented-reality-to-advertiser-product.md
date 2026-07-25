---
id: cs2325
title: AR-Enabled Catalogs: Bringing Augmented Reality to Advertiser Product Catalogs
company: Snap
primary_category: cv
sub_category: visual-search
year: 2022
source_url: https://eng.snap.com/ar-enabled-catalogs
tags: [ar, visual-search, advertising, ecommerce, object-detection, 3d]
---

# AR-Enabled Catalogs: Bringing Augmented Reality to Advertiser Product Catalogs
**Snap** · 2022 · [source](https://eng.snap.com/ar-enabled-catalogs)

## Problem
Most advertisers can't produce AR assets (3D models, try-on experiences) for their products in-house; they rely on third-party AR/3D providers. But Snap's catalog ingestion assumed a single product feed per advertiser, so there was no way to attach externally produced AR assets to existing catalog products without advertisers restructuring their entire data feeds.

## Approach / System design
Snap extended its product catalog platform to a two-feed model:
- **Primary feed**: the advertiser's existing feed with required product metadata (title, description, price, etc.).
- **Supplemental feed**: a new feed type containing only AR assets plus product IDs that match entries in the primary feed — typically supplied by the advertiser's AR partner.
The ingestion pipeline (orchestrated with Temporal) runs: download file → ingest and partition → submit via gRPC to the core catalog service → persist to the database → surface products through a vending service to downstream consumers. Supplemental feeds get an extra verification step confirming the primary feed uploaded successfully before merging.

Field provenance is tracked with Google Protobuf's FieldMask: each product record carries a signature of which fields came from which feed, enabling selective merging of supplemental data into primary records.

## Key decisions
- Add a supplemental feed type instead of forcing advertisers (or their AR partners) to modify the primary feed — zero disruption to existing integrations.
- Use FieldMask to record per-field ownership so merges are precise and auditable.
- Enforce strict precedence: primary feed values always override supplemental values, and when a primary update overwrites supplemental data the FieldMask is updated to reflect the new ownership.
- Make supplemental feeds additive-only: they can add AR data but never remove or modify primary-feed values.

## Stack
Temporal (workflow orchestration for feed ingestion), gRPC (service communication), Google Protobuf with FieldMask (serialization and field-provenance tracking), core catalog service, database persistence layer, vending service for downstream surfacing.

## Results
Launched in early 2022 with adoption by many advertisers, enabling AR try-on and product visualization experiences sourced from third-party AR providers to appear against existing catalog products. No quantitative metrics are disclosed.

## Takeaways
- Retrofitting a single-source system for multi-source data is fundamentally a provenance problem; FieldMask gave a clean per-field ownership mechanism.
- Clear, simple precedence rules (primary always wins; supplemental is additive-only) prevent merge conflicts from ever reaching advertisers.
- Meeting partners where they are — letting AR vendors ship a minimal ID+assets feed — removed the adoption barrier that a feed-restructuring requirement would have created.
