---
id: cs2163
title: "ADORE: Autonomous Domain-Oriented Relevance Engine for E-commerce"
company: JD.com
primary_category: search
sub_category: relevance-eval
year: 2025
source_url: https://arxiv.org/abs/2512.02555
tags: [relevance, LLM, knowledge-distillation, adversarial-data, chain-of-thought, e-commerce, SIGIR]
---

# ADORE: Autonomous Domain-Oriented Relevance Engine for E-commerce
**JD.com** · 2025 · [source](https://arxiv.org/abs/2512.02555)

## Problem
E-commerce search relevance modeling is squeezed from both sides: term-matching methods like BM25 suffer semantic gaps, while neural relevance models depend on domain-specific training data that is scarce and expensive to annotate manually.

## Approach / System design
ADORE is a self-sustaining relevance pipeline with three integrated modules. Rule-aware Relevance Discrimination uses Chain-of-Thought LLM prompting to generate intent-aligned training annotations, then refines the annotator with Kahneman-Tversky Optimization (KTO) so labels reflect actual user behavior patterns. Error-type-aware Data Synthesis automatically generates adversarial examples targeting known error categories to harden the model against edge cases. Key-attribute-enhanced Knowledge Distillation transfers domain attribute hierarchies from the LLM teacher into a compact student model that is deployable in production serving.

## Key decisions
- Automate both annotation (CoT prompting) and hard-case generation (adversarial synthesis) to break the manual-labeling bottleneck.
- Align the LLM annotator with user behavior via KTO rather than trusting raw prompted judgments.
- Distill into a student model with key-attribute knowledge injected, so domain structure survives the compression to a servable model.

## Stack
LLM-based CoT annotation, KTO preference fine-tuning, adversarial data synthesis, and knowledge distillation into a production student model for JD.com search relevance. Accepted to SIGIR 2025.

## Results
Large-scale experiments and online A/B testing on JD.com's advertising search verified ADORE's effectiveness; the abstract does not report specific metric numbers.

## Takeaways
A relevance system can bootstrap its own training data end to end — annotate with a behavior-aligned LLM, stress-test with synthesized adversarial cases, and distill for serving. The framework treats data production, robustness, and deployability as one loop rather than three separate projects, a resource-efficient paradigm for industrial relevance modeling.
