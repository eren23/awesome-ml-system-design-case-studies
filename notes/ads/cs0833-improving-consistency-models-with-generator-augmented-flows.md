---
id: cs0833
title: Improving Consistency Models with Generator-Augmented Flows
company: Criteo
primary_category: ads
sub_category: ctr-prediction
year: 2025
source_url: https://medium.com/criteo-engineering/improving-consistency-models-with-generator-augmented-flows-abc2ae135506
tags: [ad ranking, targeting, content personalization]
---

# Improving Consistency Models with Generator-Augmented Flows
**Criteo** · 2025 · [source](https://medium.com/criteo-engineering/improving-consistency-models-with-generator-augmented-flows-abc2ae135506)

## Problem
Diffusion models produce high-quality images but need many iterative denoising steps, which is too slow for real-time generative use cases such as personalized ad creative. Consistency Models (CMs) promise single-step (or few-step) sampling, but training them from scratch — rather than distilling from a pretrained diffusion model — is unstable and converges poorly.

## Approach / System design
The work centers on Generator-Augmented Flows (GAF), a modified CM training procedure. The key idea is to feed the model's own endpoint (clean-data) predictions back into the data–noise coupling that defines the training loss, lowering the stochasticity of the targets the model has to match. This narrows the gap between the easier distillation setting (which imitates a pretrained teacher) and the harder train-from-scratch setting.

## Key decisions
- Diagnose the instability as coming from an extra regularization term on the generator that appears specifically in the from-scratch regime.
- Use the model as its own guide (self-reinforcement) instead of requiring a separate pretrained diffusion teacher.
- Redesign the noise–data couplings rather than just tuning hyperparameters.

## Stack
Consistency Models / diffusion-style generative modeling. Specific frameworks and infrastructure are not detailed in the source.

## Results
The source reports faster convergence and better final quality from GAF versus standard from-scratch CM training. For Criteo's adtech setting this is framed as faster/cheaper training (less GPU) and more diverse generated ad variations. No precise benchmark numbers are given in the captured content.

## Takeaways
Single-step generative models are attractive for latency-bound ad creative, but their training instability is the real blocker; injecting the model's own predictions into the training coupling is a practical lever to stabilize from-scratch training without a teacher model.
