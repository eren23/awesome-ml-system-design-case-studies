---
id: cs2248
title: Task-Oriented Conversational AI in Airbnb Customer Support
company: Airbnb
primary_category: genai
sub_category: chatbots
year: 2025
source_url: https://medium.com/airbnb-engineering/task-oriented-conversational-ai-in-airbnb-customer-support-5ebf49169eaa
tags: [task-oriented-dialogue, customer-support, conversational-ai, nlp, llm]
---

# Task-Oriented Conversational AI in Airbnb Customer Support
**Airbnb** · 2025 · [source](https://medium.com/airbnb-engineering/task-oriented-conversational-ai-in-airbnb-customer-support-5ebf49169eaa)

## Problem
Airbnb wanted to automate customer-support resolution — notably cancellations, where guests and hosts who had already agreed on a refund still needed an agent to execute it, wasting agent capacity and delaying resolution.

## Approach / System design
A multi-layer issue-detection and decision-making structure: a domain classification layer routes incoming messages to domains (trip rebooking, cancellation refunds, etc.); for mutual cancellations, a second layer runs a Q&A-based intent-understanding model plus an expected-refund-ratio prediction model trained on historical cancellation data; a decision engine then routes the case or recommends help articles. Intent understanding is framed as a Question & Answer problem with single-choice binary classification instead of a hierarchical intent taxonomy, which unified training labels across domains/versions, scaled training data through questionnaire refinement, and handled non-structural issues better. Multi-turn dialog state tracking concatenates conversation history with the current request; to avoid O(n^4) blow-up, historical turns are scored asynchronously offline and cached, achieving 76.05% AUC at 120ms latency. A contextual bandit (epsilon-greedy, self-normalized inverse-propensity-scoring estimator) handles online exploration given low chatbot traffic.

## Key decisions
- Q&A formulation over multi-class intent classification: 93.19% vs 88.53% offline accuracy, and online conversion-prediction AUC 0.70 vs 0.64.
- RoBERTa-large (335M params) chosen as backbone after evaluating Albert, DistilBERT, MBart, and others.
- In-domain masked-LM pre-training on a 1.08GB corpus of conversations, listings, and help articles in 14 languages (56% English): 84.60% downstream AUC vs 82.92% without.
- Cross-domain fine-tuning on the RACE dataset for logical-reasoning cases (micro F1 to 65.69%); XLM-RoBERTa with translated labels for multilingual support (English 92.79% AUC, Spanish 91.21%, French 90.49%, Portuguese 92.32%).
- GPU serving instead of CPU to hit latency targets.

## Stack
PyTorch, HuggingFace Transformers, RoBERTa-large / XLM-RoBERTa, AWS GPU instances (p3.2xlarge), contextual-bandit reinforcement learning for online optimization.

## Results
GPU inference cut latency from 150-500ms on CPU to ~50-85ms typical (97ms p95, 120ms p99); in production the GPU switch made single transforms 3x and batch transforms 5x faster (~60ms p95). Multilingual models with translated training data significantly outperformed English-only approaches across all tested languages.

## Takeaways
Problem formulation mattered more than model choice for long-term performance — the Q&A reframing was the biggest win. Transfer learning at every level (in-domain pre-training, cross-domain fine-tuning, multilingual models) compounded gains. With traffic volumes far below search-ranking scale, contextual bandits were essential for continuous improvement where classic multivariate testing wasn't viable.
