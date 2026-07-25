---
id: cs2256
title: "CFRecs: Counterfactual Recommendations on Real Estate User Listing Interaction Graphs"
company: Zillow
primary_category: graph
sub_category: gnn
year: 2026
source_url: https://arxiv.org/abs/2602.05861
tags: [counterfactual-recommendations, graph-VAE, GNN, user-listing-graph, real-estate, actionable-recommendations]
---

# CFRecs: Counterfactual Recommendations on Real Estate User Listing Interaction Graphs
**Zillow** · 2026 · [source](https://arxiv.org/abs/2602.05861)

## Problem
Recommender systems in real estate are typically opaque: they rank listings but do not tell buyers or sellers what would need to change for a different outcome. Zillow wanted interpretable, actionable recommendations — identifying a counterfactual graph that is close to the original user–listing interaction graph but leads to different model predictions, so users can act on concrete, minimal changes in a competitive market.

## Approach / System design
CFRecs is a two-stage framework combining GNNs with a graph variational autoencoder. The GNN models user–listing interactions as graph-structured data; the Graph-VAE generates counterfactual modifications to graph structure and node attributes within a learned latent distribution, keeping proposed changes realistic. The system jointly optimizes two competing objectives: minimizing the size of structural/attribute changes (sparsity) while ensuring the modified graph actually flips the prediction (validity).

## Key decisions
- Represent the recommendation problem as counterfactual reasoning over a user–listing interaction graph rather than as pure ranking.
- Use a VAE component so counterfactuals are sampled from a learned distribution — producing plausible modifications instead of arbitrary graph edits.
- Balance sparsity against prediction validity as a dual optimization, so recommendations stay minimal yet impactful and therefore actionable.

## Stack
Graph neural networks and Graph variational autoencoders, evaluated on Zillow's real-world user–listing interaction data. Serving/production infrastructure details are not covered in the source.

## Results
The paper reports the effectiveness of CFRecs on Zillow's user–listing interaction dataset for both buyer and seller scenarios. Specific quantitative metrics are not covered in the source abstract.

## Takeaways
Counterfactual reasoning over interaction graphs turns black-box recommendations into actionable guidance — "what minimal change leads to a different outcome" — which is especially valuable in high-stakes, low-frequency domains like real estate. Constraining counterfactuals with a generative latent model keeps them realistic rather than merely adversarial.
