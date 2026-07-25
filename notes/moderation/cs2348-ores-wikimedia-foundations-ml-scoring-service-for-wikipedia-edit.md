---
id: cs2348
title: "ORES: Wikimedia Foundation's ML Scoring Service for Wikipedia Edit Quality and Vandalism Detection"
company: Wikimedia Foundation
primary_category: moderation
sub_category: integrity
year: 2015
source_url: https://github.com/wikimedia/ores
tags: [vandalism-detection, edit-quality, wikipedia, revscoring, real-time-scoring, wiki-reliability, online-community]
---

# ORES: Wikimedia Foundation's ML Scoring Service for Wikipedia Edit Quality and Vandalism Detection
**Wikimedia Foundation** · 2015 · [source](https://github.com/wikimedia/ores)

## Problem
Wikipedia's editors and automated tools needed a way to assess edit quality and detect vandalism at the scale and pace of a live encyclopedia. ORES (Objective Revision Evaluation Service) was built as a webserver for hosting ML scoring services, exposing model predictions about revisions to any tool or editor that needed them.

## Approach / System design
ORES centers on a scoring service that exposes ML models through a REST web API — e.g., HTTP endpoints of the form /v2/scores/{wiki}/{model}/{revid} — rather than batch processing. The models themselves come from the revscoring library, which evaluates Wikipedia revisions; ORES hosts them and serves scores on demand. An optional Redis layer caches scores for performance. Development environments are provided via Docker Compose, and the service is distributed as a Python 3 package via pip.

## Key decisions
- A hosted scoring webservice with an HTTP API, decoupling model consumers (editor tools, bots) from model implementation.
- revscoring as the model layer, with ORES as the serving layer.
- Redis-backed caching to keep repeated score lookups fast.
- Python 3 with standard packaging and containerized development.

## Stack
Python 3 (majority of the codebase), revscoring models, Redis for caching, Docker Compose for development, REST/HTTP API, plus Jupyter notebooks and small HTML/JavaScript components.

## Results
Per the catalog summary, ORES served real-time vandalism detection and edit quality assessment for Wikipedia editors and automated tools for nearly a decade. The repository is now archived read-only: ORES entered deprecation in late 2023, with the README warning the infrastructure is unmaintained and may break at any time. Wikimedia migrated scoring to the Lift Wing platform; some revscoring models were transitioned but remain unsupported, with no new training or code updates.

## Takeaways
- A simple scoring-as-a-service API let an entire ecosystem of community tools build on shared ML models.
- Early architecture choices (Python stack, Redis caching, HTTP API) proved solid for years of production service.
- Even well-designed ML infrastructure has a lifecycle: without ongoing maintenance, wholesale platform replacement (here, Lift Wing) eventually becomes the sustainable path.
