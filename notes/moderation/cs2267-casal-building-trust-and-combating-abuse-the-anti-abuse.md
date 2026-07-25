---
id: cs2267
title: "CASAL: Building Trust and Combating Abuse — The Anti-Abuse Core at LinkedIn"
company: LinkedIn
primary_category: moderation
sub_category: integrity
year: 2023
source_url: https://engineering.linkedin.com/blog/2023/casal--building-trust-and-combating-abuse---the-anti-abuse-core-
tags: [anti-abuse, real-time, nearline, scoring-library, trust-and-safety, platform-infrastructure]
---

# CASAL: Building Trust and Combating Abuse — The Anti-Abuse Core at LinkedIn
**LinkedIn** · 2023 · [source](https://engineering.linkedin.com/blog/2023/casal--building-trust-and-combating-abuse---the-anti-abuse-core-)

## Problem
LinkedIn's original monolithic abuse-scoring system struggled as the platform grew: novel adversarial attacks required fast defensive iteration, and every new product launch added operational overhead. The company needed a scalable, shared foundation for detecting and acting on abuse — fake accounts, account takeover, content abuse — across all surfaces.

## Approach / System design
CASAL (Centralized Abuse Scoring As a Library) is a shared framework supporting both synchronous (real-time) and asynchronous (nearline) abuse-detection workflows. Teams author isolated decision workflows per abuse vector on top of common components:
- **Feature collection**: parallel signal retrieval from microservices and stores (Espresso, Venice, Rest.li endpoints, Couchbase), with caching for stable member attributes.
- **Scoring**: ML inference across diverse model families — logistic regression, XGBoost, isolation forests, sequence models, graph neural networks — in two modes: CURRENT (drives immediate action) and PROPOSED (experimental, shadow evaluation).
- **Business rules**: a DROOLS-based when-then rules engine layered with model scores.
- **Enforcement**: graduated actions from CAPTCHA challenges up to account restrictions.
- **Tracking**: Kafka event streams log every decision for auditing and model feedback.

## Key decisions
- Replace the monolith with library-based, decentralized per-vector workflows, avoiding noisy-neighbor effects and reducing operational overhead.
- Separate CURRENT vs. PROPOSED scoring so experiments run against production traffic without enforcement risk.
- Combine ML with a rules engine and human review — automation for pattern recognition, humans for contextual edge cases.
- Keep offline training (Azkaban/Hadoop) decoupled from online inference, and allow new defenses to ship without service redeployment.

## Stack
Kafka, DROOLS rules engine, Espresso, Venice, Couchbase, Rest.li, Azkaban and Hadoop for offline training, TREX (LinkedIn's A/B testing platform), and an in-house MLOps/monitoring platform.

## Results
The post is qualitative: real-time risk assessment across surfaces, significantly reduced operational overhead, and the ability to deploy new defenses immediately without redeployment cycles. Specific quantitative metrics are not covered in the source.

## Takeaways
A shared scoring library with per-vector workflow isolation scales trust-and-safety engineering better than either a monolith or fully independent systems. Sustained effectiveness depends on feedback loops (abuse reports, reviewer input), periodic retraining against an evolving threat landscape, and deliberate human–AI division of labor.
