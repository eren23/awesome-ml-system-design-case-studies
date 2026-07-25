---
id: cs2274
title: LLM-Ensemble: Optimal Large Language Model Ensemble Method for E-commerce Product Attribute Value Extraction
company: Walmart
primary_category: nlp
sub_category: information-extraction
year: 2024
source_url: https://arxiv.org/abs/2403.00863
tags: [llm-ensemble, attribute-extraction, e-commerce, product-attributes, sigir, knowledge-distillation, llama2, gpt-4]
---

# LLM-Ensemble: Optimal Large Language Model Ensemble Method for E-commerce Product Attribute Value Extraction
**Walmart** · 2024 · [source](https://arxiv.org/abs/2403.00863)

## Problem
Accurate product attribute value extraction underpins recommendations and customer experience in e-commerce. Individual LLMs perform well but exhibit different strengths and weaknesses depending on their data, architectures, and hyperparameters — no single model dominates across attributes and products.

## Approach / System design
LLM-Ensemble: instead of picking one model, aggregate attribute predictions from multiple LLMs. The algorithm iteratively learns per-model weights and combines the models' label outputs into a final attribute value. The authors position the method as theoretically optimal for this aggregation, computationally efficient, quickly convergent, and safe for production deployment.

## Key decisions
- Ensemble across heterogeneous LLM providers/sizes (Llama2-13B, Llama2-70B, PaLM-2, GPT-3.5, GPT-4) to exploit complementary strengths.
- Learn ensemble weights iteratively rather than using static voting.
- Validate with production A/B tests on business metrics, not just offline extraction accuracy.

## Stack
Llama2-13B, Llama2-70B, PaLM-2, GPT-3.5, and GPT-4 as ensemble members; learned weighted aggregation; evaluated on Walmart's internal attribute-extraction dataset.

## Results
- Outperformed every individual state-of-the-art LLM on Walmart's internal dataset.
- Deployed to production; A/B tests showed improvements in GMV, CTR, CVR, and add-to-cart rate (specific magnitudes not given in the abstract).

## Takeaways
When LLMs disagree in systematic, model-specific ways, learned ensembling captures value no single model provides — and the offline accuracy gain carried through to core commercial metrics in production. The practical bar for deployment (efficiency, fast convergence, safety) shaped the algorithm as much as optimality claims.
