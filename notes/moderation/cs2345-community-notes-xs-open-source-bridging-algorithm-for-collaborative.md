---
id: cs2345
title: "Community Notes: X's Open-Source Bridging Algorithm for Collaborative Misinformation Labeling"
company: X (formerly Twitter)
primary_category: moderation
sub_category: policy-enforcement
year: 2022
source_url: https://github.com/twitter/communitynotes
tags: [misinformation, bridging-algorithm, matrix-factorization, open-source, crowdsourced-moderation, ranking]
---

# Community Notes: X's Open-Source Bridging Algorithm for Collaborative Misinformation Labeling
**X (formerly Twitter)** · 2022 · [source](https://github.com/twitter/communitynotes)

## Problem
Misleading posts spread at platform scale, and centralized fact-checking neither scales nor commands broad trust. Community Notes empowers people on X to add context notes to potentially misleading posts — but crowdsourced notes need a scoring mechanism that surfaces genuinely helpful notes rather than notes that merely win a partisan majority vote.

## Approach / System design
The core is a note scoring algorithm (in the repository's scoring module) that determines which contributed notes are shown as helpful, based on contributor ratings. Per the catalog summary, this is a bridging-based matrix factorization approach: notes are selected for cross-ideological appeal — rated helpful by contributors who typically disagree — rather than by raw vote counts. The repository accompanies the algorithm with a research paper detailing its development, separates concerns into distinct modules for note generation (a template API), evaluation, and scoring, and publishes daily public data releases of all notes, ratings, and contributor information so outsiders can reproduce scoring.

## Key decisions
- Bridging-based ranking over majority voting, requiring agreement across normally-disagreeing rater groups.
- Open-sourcing the scoring algorithm for transparency and reproducibility, with daily public data drops.
- Maintaining the core algorithm in an internal repository and exporting updates to GitHub, balancing production stability with openness.
- Country-by-country geographic expansion to respect local nuance.
- Modular separation of note generation, evaluation, and scoring.

## Stack
Python (roughly 90% of the codebase, requiring Python 3.10+) with Jupyter notebooks for analysis; matrix-factorization-based scoring per the catalog summary; public datasets released daily.

## Results
The system operates at platform scale on X, with published peer-reviewed research documenting outcomes and performance analysis, and full transparency via daily data releases. Specific effectiveness metrics are not stated in the repository README.

## Takeaways
- Bridging-based scoring is a viable production alternative to majority voting for crowdsourced moderation, selecting content with cross-perspective appeal.
- Transparency infrastructure — open code plus reproducible public data — builds trust in a system that labels contested content.
- Keeping the production algorithm internal while exporting to a public mirror balances stability with openness.
