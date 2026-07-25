---
id: cs2269
title: Federated Anti-Abuse Defense Ecosystem Using AI at LinkedIn
company: LinkedIn
primary_category: moderation
sub_category: integrity
year: 2024
source_url: https://www.linkedin.com/blog/engineering/talent/federated-anti-abuse-defense-ecosystem-using-ai-migration
tags: [federated, anti-abuse, ecosystem, trust-and-safety, cross-surface, platform-migration]
---

# Federated Anti-Abuse Defense Ecosystem Using AI at LinkedIn
**LinkedIn** · 2024 · [source](https://www.linkedin.com/blog/engineering/talent/federated-anti-abuse-defense-ecosystem-using-ai-migration)

## Problem
LinkedIn's legacy anti-abuse infrastructure was a single monolithic service scoring all abuse vectors. At 1B+ members with evolving threats, it hit business-logic overhead, hardware limitations, noisy-neighbor interference between workloads, and developer-productivity problems — one team's heavy workflow could degrade every other defense sharing the service.

## Approach / System design
The team migrated the monolith to a federated ecosystem via a three-pronged approach:
1. **CASAL library**: common scoring functionality and interfaces extracted into a shared library.
2. **Federated clusters**: scoring workflows split by abuse vector (fake profiles, content moderation, spam, harassment, etc.), each with dedicated clusters and independent team ownership.
3. **Isolated online/nearline workflows**: decision-making separated from data-collection systems, decoupling business logic from data management so defense mechanisms aren't contaminated by pipeline concerns.

The migration itself ran production traffic through new services in a non-action validation mode — scoring without enforcing — with Kafka events enabling detailed old-vs-new comparison, followed by a slow, automated-validation-backed traffic ramp.

## Key decisions
- Federate by abuse vector rather than scale the monolith, gaining resource isolation and independent ownership.
- Standardize on a shared library (CASAL) so federation doesn't mean reimplementation.
- Validate with shadow (non-action) traffic and gradual ramps to keep member safety intact throughout a multi-month migration.
- Invest in automated validation and CI/CD integration instead of manual comparison.

## Stack
CASAL shared scoring library, per-vector service clusters, Kafka for validation event comparison, online and nearline scoring workflows, CI/CD automation. Specific model details are not covered in the source.

## Results
- Hardware scaling constraints resolved through per-vector resource isolation.
- Noisy-neighbor performance degradation between abuse workflows eliminated.
- Faster team iteration via independent code ownership.
- Migration completed with zero impact to member safety.

## Takeaways
A federated ecosystem on a shared core beats both a monolith and fully siloed systems for trust-and-safety at scale. Big migrations are also design opportunities — and they succeed on the unglamorous parts: shadow validation, comprehensive system and business metric monitoring with anomaly detection, automation, and tight alignment across product, AI, and SRE teams.
