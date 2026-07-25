---
id: cs2195
title: New Approaches For Detecting AI-Generated Profile Photos
company: LinkedIn
primary_category: cv
sub_category: object-detection
year: 2023
source_url: https://www.linkedin.com/blog/engineering/trust-and-safety/new-approaches-for-detecting-ai-generated-profile-photos
tags: [ai-generated-image-detection, deepfake-detection, EfficientNet, PCA, autoencoder, GAN-detection, StyleGAN, face-detection, trust-and-safety]
---

# New Approaches For Detecting AI-Generated Profile Photos
**LinkedIn** · 2023 · [source](https://www.linkedin.com/blog/engineering/trust-and-safety/new-approaches-for-detecting-ai-generated-profile-photos)

## Problem
Fake LinkedIn profiles increasingly use AI-generated synthetic face photos that most members cannot visually distinguish from real ones, threatening platform authenticity. LinkedIn needed detection techniques reliable enough to operate on a network with hundreds of millions of daily users, where even a small false-positive rate would wrongly flag huge numbers of legitimate photos.

## Approach / System design
LinkedIn's Trust Data team partnered with UC Berkeley's Hany Farid (via the LinkedIn Scholars program) on embedding-based detectors. The core insight: GAN-generated faces share a highly regular facial structure — averaging many synthetic faces yields sharp, clear facial features, while averaging real photos produces a blur because of natural variation in pose and framing. Two complementary learned embeddings exploit this regularity: a PCA-based linear embedding and an autoencoder-based embedding, with a Fourier-based fixed embedding used as a baseline to show that generic, non-learned representations fail at the task. Models were trained on 100,000 real LinkedIn profile photos plus 41,500 synthetic faces spanning five synthesis engines: StyleGAN1, StyleGAN2, StyleGAN3, Generated.photos, and Stable Diffusion.

## Key decisions
- Chose lightweight learned embeddings (PCA, autoencoder) over heavier CNN forensic classifiers, betting on the structural regularity of GAN faces rather than low-level pixel artifacts.
- Trained on real production profile photos rather than only public datasets, matching the deployment distribution.
- Evaluated cross-generator generalization explicitly: models trained on StyleGAN variants partially transferred to Generated.photos (also GAN-based) but not to Stable Diffusion, reflecting the architectural gap between GANs and diffusion models.
- Set operating points around a strict ~1% false-positive budget appropriate for trust-and-safety at scale.

## Stack
PCA-based linear embedding, autoencoder embedding, Fourier-based fixed-embedding baseline; comparison against state-of-the-art CNN-based forensic classifiers; training corpus of LinkedIn profile photos plus StyleGAN1/2/3, Generated.photos, and Stable Diffusion synthetic faces.

## Results
- 99.6% true-positive rate detecting synthetic StyleGAN faces at only a 1% false-positive rate on real photos.
- Outperformed state-of-the-art CNN forensic classifiers, notably on StyleGAN3 where CNN approaches struggled significantly.
- Partial generalization to unseen GAN engines; diffusion-generated faces (Stable Diffusion) remained out of scope for the GAN-trained detectors.

## Takeaways
Simple, lightweight embedding models can match or beat complex CNNs for a face-specific forensic task when they encode the right structural prior. Cross-architecture generalization is the hard part — GAN-trained detectors do not transfer to diffusion imagery, so detection portfolios must evolve with generator technology. Academia-industry collaboration accelerated moving forensic research into production-scale defense.
