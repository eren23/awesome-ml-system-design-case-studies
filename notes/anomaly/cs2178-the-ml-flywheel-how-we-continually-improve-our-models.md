---
id: cs2178
title: "The ML Flywheel: How We Continually Improve Our Models to Reduce Card Testing"
company: Stripe
primary_category: anomaly
sub_category: outlier-detection
year: 2024
source_url: https://stripe.com/blog/the-ml-flywheel-how-we-continually-improve-our-models-to-reduce-card-testing
tags: [card-testing, ml-flywheel, continuous-learning, multi-level-models, feature-engineering, flyte]
---

# The ML Flywheel: How We Continually Improve Our Models to Reduce Card Testing
**Stripe** · 2024 · [source](https://stripe.com/blog/the-ml-flywheel-how-we-continually-improve-our-models-to-reduce-card-testing)

## Problem
Card testing — fraudsters validating stolen card numbers (verification) or guessing them (enumeration) via small or zero-dollar transactions — is a small share of volume but highly damaging once validated cards are resold or used for large purchases. Attacks evolve constantly and lack explicit labels (unlike disputes), making supervised detection hard to keep current.

## Approach / System design
Stripe layers models at three abstraction levels that work together to adjust blocking thresholds dynamically in real time: a macro level estimating overall card-testing prevalence across the platform daily; a meso level identifying which businesses, issuers, or surfaces are under attack; and a micro level scoring individual transactions from diverse signals. Around the models sits a continuous-improvement flywheel: attack intelligence is consolidated, patterns are discovered automatically and reviewed by experts to mint labels, and models are retrained rapidly so reactive discoveries become proactive detections within hours. Large transformer foundation models trained on billions of transactions complement smaller specialized classifiers via compressed embeddings.

## Key decisions
- Multi-scale modeling (platform → merchant/issuer → transaction) instead of a single transaction scorer, enabling precise intervention with fewer false positives.
- Built a rapid labeling-and-retraining cycle combining attack intel, automated pattern discovery, and manual expert review to compensate for missing ground-truth labels.
- Augmented specialized models with transaction foundation-model embeddings to catch novel or subtle attacks on high-volume businesses.

## Stack
Shepherd for feature engineering (built in partnership with Airbnb), Flyte for ML orchestration, specialized card-testing classifiers plus large transformer foundation models over billions of transactions.

## Results
Successful card testing attacks on Stripe declined by 80% over two years, even as payment volume grew past $1 trillion annually.

## Takeaways
Sustained fraud reduction comes from the flywheel, not any single model: systematic labeling frameworks, fast experimentation infrastructure, modeling at multiple granularities, and pairing specialized classifiers with foundation-model representations.
