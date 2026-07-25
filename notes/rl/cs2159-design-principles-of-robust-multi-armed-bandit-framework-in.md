---
id: cs2159
title: Design Principles of Robust Multi-Armed Bandit Framework in Video Recommendations
company: Amazon Prime Video
primary_category: rl
sub_category: bandits
year: 2023
source_url: https://arxiv.org/abs/2310.01419
tags: [multi-armed-bandit, video-recommendations, item-cannibalization, robustness, streaming]
---

# Design Principles of Robust Multi-Armed Bandit Framework in Video Recommendations
**Amazon Prime Video** · 2023 · [source](https://arxiv.org/abs/2310.01419)

## Problem
Bandit research for recommenders focuses heavily on exploration strategies while underweighting exploitation-side failure modes that dominate in production: distributional shift in time-variant metadata signals, item cannibalization (near-duplicate items competing for the same impressions), and unstable weight estimates caused by data sparsity.

## Approach / System design
Drawing on production experience with video recommendations, the authors codify design principles for building bandit frameworks that stay robust under real-world dynamics. They target three vulnerabilities — sensitivity to time-varying metadata, cannibalization among similar items, and weight fluctuation under sparse feedback — and systematically evaluate the bandit design choices that mitigate each, using experiments and case studies against baselines that omit those choices.

## Key decisions
- Treat robustness of exploitation, not just quality of exploration, as a first-class design goal.
- Evaluate concrete design choices (rather than a single new algorithm) so the principles transfer across bandit implementations.
- Address popularity bias explicitly, improving fairness of exposure between popular and unpopular content.

## Stack
Multi-armed bandit recommendation framework for a video streaming service; validated through empirical experiments and case studies with comparative baselines. Specific serving infrastructure is not covered in the source.

## Results
Against baseline bandit models lacking the proposed design choices, improvements reached up to 11.88% in ROC-AUC and 44.85% in PR-AUC.

## Takeaways
A bandit that works in a paper can still wobble in production; robustness has to be designed in against drift, cannibalization, and sparsity. Codified design principles — not exotic exploration policies — delivered the large measurable gains, and they double as a fairness lever for less-popular content.
