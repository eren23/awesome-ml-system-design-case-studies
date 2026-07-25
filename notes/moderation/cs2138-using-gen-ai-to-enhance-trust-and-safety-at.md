---
id: cs2138
title: Using Gen AI to Enhance Trust and Safety at Thumbtack: Applying a Fine-Tuned LLM Model to Review Messages
company: Thumbtack
primary_category: moderation
sub_category: integrity
year: 2025
source_url: https://medium.com/thumbtack-engineering/using-genai-to-enhance-trust-and-safety-at-thumbtack-2b8355556f1f
tags: [llm, fine-tuning, two-tier, cnn, message-moderation, trust-safety, production]
---

# Using Gen AI to Enhance Trust and Safety at Thumbtack: Applying a Fine-Tuned LLM Model to Review Messages
**Thumbtack** · 2025 · [source](https://medium.com/thumbtack-engineering/using-genai-to-enhance-trust-and-safety-at-thumbtack-2b8355556f1f)

## Problem
Thumbtack needs to catch policy violations in messages between customers and professionals on its home-services marketplace. Rules caught the obvious cases (offensive language, job-seeking, partnership solicitations), but nuanced violations — sarcasm, implied threats, context-dependent abuse — slipped through, and the incumbent CNN classifier wasn't accurate enough for production enforcement.

## Approach / System design
A staged pipeline: a rule-based engine handles obvious violations; a fine-tuned LLM classifies the hard, contextual cases; flagged messages go to a manual review queue. Two production-critical additions:
- The legacy CNN was repurposed as a pre-filter (with adjusted threshold) so only ~20% of message volume reaches the LLM, controlling cost.
- A centralized LLM service built on LangChain, so other teams can reuse the same infrastructure.

## Key decisions
- Abandoned prompt engineering after it only reached 0.56 AUC; switched to fine-tuning on tens of thousands of labeled samples.
- Kept the old CNN as a cost-optimization filter instead of throwing it away.
- Invested in a shared LLM service rather than a one-off integration.

## Stack
Fine-tuned LLM (base model not specified), legacy CNN pre-filter, LangChain-based centralized LLM service, rule-based engine, human review queue.

## Results
- Fine-tuned model: 0.93 AUC vs 0.56 for the prompt-engineered baseline.
- In production: 3.7x precision improvement and 1.5x better recall, across tens of millions of messages.

## Takeaways
- For domain-specific classification, fine-tuning decisively beat prompt engineering (0.56 → 0.93 AUC).
- Legacy models still earn their keep as cheap pre-filters in front of expensive LLM calls.
- Centralizing LLM serving turns a single project into reusable company infrastructure.
