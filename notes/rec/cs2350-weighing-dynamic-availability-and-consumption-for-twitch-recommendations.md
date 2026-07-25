---
id: cs2350
title: Weighing dynamic availability and consumption for Twitch recommendations
company: Twitch
primary_category: rec
sub_category: candidate-generation
year: 2022
source_url: https://www.amazon.science/publications/weighing-dynamic-availability-and-consumption-for-twitch-recommendations
tags: [live-streaming, implicit-feedback, loss-weighting, availability-bias, negative-sampling, collaborative-filtering]
---

# Weighing dynamic availability and consumption for Twitch recommendations
**Twitch** · 2022 · [source](https://www.amazon.science/publications/weighing-dynamic-availability-and-consumption-for-twitch-recommendations)

## Problem
Twitch recommendations are trained on implicit feedback from watch history, which is heavily biased in a live-streaming setting. Most apparent "negative" examples arise simply because the user and the channel were not online at the same time — not because the user disliked the channel. Positive signals are also hard to calibrate, since watch sessions vary widely in duration.

## Approach / System design
The researchers introduce two loss weighting methods applied during recommendation model training. Availability weighting down-weights negative examples that can be explained by user-channel availability mismatch, so the model stops learning dispreference from co-absence. Consumption weighting scales the importance of positive examples by minutes watched, calibrating how strongly each watch session counts as an endorsement. Evaluation metrics were also modified to align with the weighted objectives, and the methods were validated offline before an online A/B test.

## Key decisions
- Fix the bias in the loss function rather than in the candidate set: keep the implicit-feedback data but reweight it.
- Explicitly model the dynamic availability of both sides (viewer online-time and streamer broadcast-time) as the dominant source of false negatives.
- Use watch duration as a graded positive signal instead of treating all watches equally.
- Align offline evaluation metrics with the new weighting so offline results predict online behavior.

## Stack
Not covered in the source.

## Results
An A/B test showed a 7.9% sitewide increase in recommended minutes watched, and offline experimentation confirmed the effectiveness of both weighting schemes.

## Takeaways
In live platforms, absence of interaction is usually absence of opportunity, not absence of interest. Explicitly modeling availability in the training loss — and grading positives by consumption intensity — corrects biases that standard implicit-feedback collaborative filtering bakes in, and the correction is cheap because it changes only loss weights, not architecture.
