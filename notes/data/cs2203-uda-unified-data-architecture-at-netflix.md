---
id: cs2203
title: "UDA: Unified Data Architecture at Netflix"
company: Netflix
primary_category: data
sub_category: data-pipeline
year: 2025
source_url: https://netflixtechblog.com/uda-unified-data-architecture-6a6aee261d8d
tags: [knowledge-graph, RDF, SHACL, domain-modeling, schema-projection, GraphQL, Avro, data-containers, ML-pipelines, upper-metamodel]
---

# UDA: Unified Data Architecture at Netflix
**Netflix** · 2025 · [source](https://netflixtechblog.com/uda-unified-data-architecture-6a6aee261d8d)

## Problem
Core business concepts like "actor" or "movie" were modeled independently in system after system with no coordination. That fragmentation produced duplicated models across teams, inconsistent terminology (the same word meaning different things), hard-to-detect data quality issues like broken references, and weak connectivity — relationships between data barely existed across system boundaries.

## Approach / System design
UDA (Unified Data Architecture) is a knowledge graph that connects domain models to the data containers holding the actual data. Teams model a domain once; UDA then transpiles that model into GraphQL, Avro, SQL, RDF, and Java schemas ("projections"), catalogs mappings from model elements down to individual columns or GraphQL fields, and automates faithful data movement between containers via Data Mesh and CDC into Iceberg tables. Concepts are discoverable through search and graph traversal, and programmatically introspectable via Java, GraphQL, or SPARQL. At the base sits "Upper," a self-referencing upper metamodel — the model for all models — that is self-describing, self-validating, and conforms to its own definition. The information model is named-graph-first: every named graph conforms to a governing model, giving modularity and governance.

## Key decisions
- Built on RDF and SHACL for semantics and validation, but extended them significantly: stock RDF lacked an enterprise-governance information model, and SHACL couldn't express local schemas and typed keys as used in real systems.
- Invented the Upper metamodel to bootstrap governance — all domain models are themselves data conforming to Upper.
- Modeled data containers (GraphQL resolvers, Data Mesh sources, Iceberg tables) as system domains so systems themselves are represented in the graph.
- Made mappings first-class to enable "intent-based automation": UDA reasons out how to move data without consumers specifying pipelines.
- Derived schemas, pipelines, and queries from domain models rather than maintaining them by hand.

## Stack
RDF + SHACL, custom Upper metamodel, Jena-based Java API, GraphQL services, transpilation to GraphQL/Avro/SQL/RDF/Java, Data Mesh + CDC for movement, Iceberg tables for storage, SKOS for controlled vocabularies, SPARQL for introspection.

## Results
No quantitative metrics are reported. Early adopters: Primary Data Management (controlled vocabularies/taxonomies with auto-provisioned business-user UI and generated Avro/GraphQL schemas) and Sphere (self-service operational reporting where business users walk the graph and SQL is generated automatically, no manual joins). The unified semantic foundation also feeds ML pipelines.

## Takeaways
Modeling domains once and projecting everywhere replaces N independent models with one governed source of semantics. Standards like RDF/SHACL get you started but need real engineering investment to fit enterprise governance. A self-referential metamodel gives the system a principled way to evolve, and mappings-as-data turn integration work into automated reasoning.
