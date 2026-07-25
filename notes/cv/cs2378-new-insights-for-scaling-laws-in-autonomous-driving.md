---
id: cs2378
title: New Insights for Scaling Laws in Autonomous Driving
company: Waymo
primary_category: cv
sub_category: object-detection
year: 2025
source_url: https://waymo.com/blog/2025/06/scaling-laws-in-autonomous-driving/
tags: [autonomous-driving, scaling-laws, perception, computer-vision, self-driving]
---

# New Insights for Scaling Laws in Autonomous Driving
**Waymo** · 2025 · [source](https://waymo.com/blog/2025/06/scaling-laws-in-autonomous-driving/)

## Problem
Scaling laws — bigger models, more data, more compute yielding predictably better performance — are established for LLMs, but it was unclear whether they hold for autonomous-vehicle capabilities like motion forecasting and planning, which involve messy real-world uncertainty and long-tail edge cases. Without that evidence, investing in larger AV models and datasets is a gamble.

## Approach / System design
Waymo ran a comprehensive scaling study on its internal dataset of 500,000 hours of driving. They trained model families and measured how motion forecasting and planning quality change with training compute, dataset size, and inference compute, evaluating with open-loop metrics as well as closed-loop simulation that better reflects real driving behavior.

## Key decisions
- Focused the study on two core AV capabilities: motion forecasting and planning.
- Scaled along three axes independently — training compute, data volume, inference compute.
- Validated in closed-loop simulation rather than relying only on open-loop metrics, to connect scaling to real-world driving performance.

## Stack
Deep learning models spanning roughly 1M to 30M parameters trained on Waymo's internal driving dataset; closed-loop simulation environments; multimodal foundation models referenced as the broader research direction. Specific architectures are not detailed.

## Results
- Motion forecasting quality follows a power law in training compute, mirroring LLM scaling behavior.
- Data scaling proved critical to performance improvement, and scaling inference compute improved handling of challenging driving scenarios.
- Closed-loop performance showed similar scaling trends — presented as the first evidence that real-world AV performance improves predictably with more training data and compute.

## Takeaways
AV development can borrow the LLM playbook: predictable power-law scaling justifies confident investment in larger datasets, models, and inference budgets to improve safety and behavioral sophistication. The findings likely extend beyond driving to robotics and embodied AI.
