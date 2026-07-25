---
id: cs1774
title: Practice on Long Behavior Sequence Modeling in Tencent Advertising
company: Tencent
primary_category: ads
sub_category: ctr-prediction
year: 2025
source_url: https://arxiv.org/abs/2510.21714
tags: [long-sequence, cross-domain, temporal-interest, wechat]
---

# Practice on Long Behavior Sequence Modeling in Tencent Advertising
**Tencent** · 2025 · [source](https://arxiv.org/abs/2510.21714)

## Problem
Ad-domain user behavior is sparse, so no single domain yields behavior sequences long enough for effective interest modeling. Fusing behaviors across advertising scenarios and content domains fixes the sparsity but introduces three new problems: feature-taxonomy gaps between scenarios and domains, interference between fields (inter-field interference), and interference between different advertising objectives (target-wise interference).

## Approach / System design
Tencent unifies cross-domain behavior into commercial trajectories and models them with a two-stage framework. Stage one is search/retrieval over the long sequence: a hierarchical hard search handles complex feature taxonomies, while a decoupled embedding-based soft search reduces conflicts between attention and representation learning. Stage two is sequence modeling on the retrieved behaviors: Decoupled Side Information Temporal Interest Networks (TIN), Target-Decoupled Positional Encoding, Target-Decoupled SASRec, and Stacked TIN to capture high-order behavioral correlations.

## Key decisions
- Integrate behavior across advertising scenarios and content domains into a single unified commercial trajectory rather than modeling each domain separately.
- Adopt a two-stage search-then-model design so full long sequences never hit the heavy attention model directly.
- Apply decoupling systematically — side information, positional encoding, and per-target components — to neutralize inter-field and target-wise interference.

## Stack
Not covered in the source.

## Results
Deployed in production across Tencent's platforms: 4.22% GMV lift on WeChat Channels and 1.96% GMV increase on WeChat Moments.

## Takeaways
Cross-domain fusion is the practical route to long behavior sequences in sparse ad domains, but it only pays off if the interference it introduces is explicitly decoupled — across feature taxonomies, fields, and optimization targets.
