---
id: cs2083
title: "LBM: Hierarchical Large Auto-Bidding Model via Reasoning and Acting"
company: Kuaishou
primary_category: ads
sub_category: bidding
year: 2026
source_url: https://arxiv.org/abs/2603.05134
tags: [auto-bidding, LLM, reasoning, hierarchical-model, reinforcement-learning, bidding-strategy]
---

# LBM: Hierarchical Large Auto-Bidding Model via Reasoning and Acting
**Kuaishou** · 2026 · [source](https://arxiv.org/abs/2603.05134)

## Problem
Production auto-bidding systems are opaque and generalize poorly as ad market conditions shift. Applying LLMs directly to bidding is hard: auctions demand numerical precision that free-form generation lacks, general LLMs miss specialized bidding knowledge, and hallucinated actions are costly in live auctions.

## Approach / System design
LBM is a hierarchical two-level model: LBM-Think, an LLM-based layer that performs high-level reasoning about the bidding situation, and LBM-Act, a specialized action model that turns that reasoning into concrete bidding actions. A dual embedding mechanism fuses language inputs with numerical signals so the model is language-guided but numerically grounded. Training uses GQPO, an offline reinforcement technique designed to mitigate hallucination without requiring simulators or real-world rollouts.

## Key decisions
- Separate reasoning from acting: let the LLM interpret and strategize while a specialized model emits precise actions, instead of asking one LLM to do both.
- Fuse language and numerical modalities via dual embeddings rather than serializing numbers into text.
- Fine-tune offline (GQPO) to avoid the cost and risk of live rollouts or building a high-fidelity auction simulator.

## Stack
LLM backbone for the reasoning layer, a generative action model for bidding, and offline reinforcement learning (GQPO). Specific base models and infrastructure are not covered in the source. Published at WWW 2026.

## Results
The paper reports that the generative backbone is superior to alternatives, with efficient training and improved generalization; specific production metrics are not covered in the source abstract.

## Takeaways
A practical recipe for LLMs in auction systems: keep the LLM at the strategy level, delegate precise numeric actions to a specialized head, and use offline RL to control hallucination — gaining interpretability and adaptivity without sacrificing auction-grade precision.
