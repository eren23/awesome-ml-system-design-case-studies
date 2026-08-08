---
id: cs1835
title: Cruise's Continuous Learning Machine Predicts the Unpredictable on San Francisco Roads
company: Cruise
primary_category: cv
sub_category: object-detection
year: 2020
source_url: https://medium.com/cruise/cruise-continuous-learning-machine-30d60f4c691b
tags: [autonomous-driving, prediction, self-supervised-learning, active-learning, auto-labeling]
---

# Cruise's Continuous Learning Machine Predicts the Unpredictable on San Francisco Roads
**Cruise** · 2020 · [source](https://medium.com/cruise/cruise-continuous-learning-machine-30d60f4c691b)

## Problem
Autonomous vehicle perception and prediction models fail most often on rare, long-tail scenarios that are underrepresented in training data. Manual annotation of edge-case driving footage is expensive, slow, and does not scale to the continuous stream of data collected by a fleet operating in a complex city environment like San Francisco.

## Approach / System design
The Continuous Learning Machine (CLM) generates training labels automatically by using future perception output as ground truth for past prediction targets, a form of self-supervised labeling that exploits the temporal structure of driving data. An active learning component mines the fleet's data stream for hard or unusual scenarios that would most benefit model performance, prioritizing those cases for the retraining pipeline. This loop allows models to be updated continuously as the fleet encounters new situations, without requiring human annotators for each training example.

## Key decisions
Using future perception as automatic ground truth for prediction labels eliminates the annotation bottleneck that would otherwise constrain how frequently models can be retrained. Active learning-based scenario mining is critical to ensure the automatic labels are spent on the highest-value examples rather than common, already-solved cases. Designing the system to operate continuously rather than in batch retraining cycles was necessary to keep up with a live deployed fleet.

## Stack
Self-supervised auto-labeling pipeline (future perception as ground truth), active learning for scenario mining, continuous retraining infrastructure. Specific model architectures and compute infrastructure details are not covered in the source.

## Results
Not covered in the source.

## Takeaways
Self-supervised labeling using temporal structure in sensor data is a scalable alternative to manual annotation for continuously deployed autonomous systems. Combining auto-labeling with active learning ensures the limited retraining budget is directed at the long-tail scenarios that matter most for safety and reliability.
