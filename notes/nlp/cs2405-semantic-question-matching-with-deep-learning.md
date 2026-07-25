---
id: cs2405
title: Semantic Question Matching with Deep Learning
company: Quora
primary_category: nlp
sub_category: entity-resolution
year: 2017
source_url: https://engineering.quora.com/Semantic-Question-Matching-with-Deep-Learning
tags: [question-deduplication, siamese-network, lstm, text-classification, duplicate-detection, sentence-similarity]
---

# Semantic Question Matching with Deep Learning
**Quora** · 2017 · [source](https://engineering.quora.com/Semantic-Question-Matching-with-Deep-Learning)

## Problem
Quora wants exactly one canonical page per unique question intent, so duplicate questions must be detected and merged. The task is framed as binary classification: given a question pair (q1, q2), learn f(q1, q2) → 0/1, where 1 means the questions are semantically equivalent. The production baseline was a random forest over handcrafted features.

## Approach / System design
Three deep learning architectures were explored, all built on custom word2vec embeddings trained on Quora's own corpus:
1. **LSTM with concatenation**: encode each question into a vector with an LSTM, concatenate the two vectors, and classify through dense layers.
2. **LSTM with distance and angle**: following Tai, Socher & Manning, feed the Euclidean distance between the two question vectors and their element-wise product ("angle") into a neural network classifier.
3. **Decomposable attention**: Google Research's attention approach — soft-align word pairs across the two questions, compare aligned phrases, then aggregate for the final decision; attractive for its small parameter count.

## Key decisions
- Train in-domain word embeddings on Quora's corpus rather than using off-the-shelf vectors.
- Represent the pair relationship explicitly (distance/angle features or cross-question attention) instead of only concatenating independent encodings.
- Compare against a strong production baseline: a random forest using cosine similarity, word overlap, topic labels, and part-of-speech tags.

## Stack
Word2vec embeddings, LSTM networks, decomposable attention models; random forest with handcrafted features as the production baseline.

## Results
The post compares the approaches but does not publish specific accuracy or F1 numbers. The deep learning models eliminated the iterative feature-engineering overhead of the baseline.

## Takeaways
- End-to-end learned representations can replace hand-engineered similarity features for paraphrase detection, cutting feature-engineering cost.
- Modeling the interaction between the two texts (distance metrics, attention alignment) matters more than the encoder alone.
- Planned next steps were deeper architectures and ensembling.
