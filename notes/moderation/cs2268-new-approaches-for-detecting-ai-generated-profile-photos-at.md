---
id: cs2268
title: New Approaches for Detecting AI-Generated Profile Photos at LinkedIn
company: LinkedIn
primary_category: moderation
sub_category: integrity
year: 2023
source_url: https://engineering.linkedin.com/blog/2023/new-approaches-for-detecting-ai-generated-profile-photos
tags: [deepfake, stylegan, computer-vision, fake-profile, trust-and-safety, synthetic-media]
---

# New Approaches for Detecting AI-Generated Profile Photos at LinkedIn
**LinkedIn** · 2023 · [source](https://engineering.linkedin.com/blog/2023/new-approaches-for-detecting-ai-generated-profile-photos)

## Problem
Fake-account operators increasingly use generative AI to produce convincing synthetic profile photos that human reviewers and members cannot reliably distinguish from real headshots. LinkedIn needed an automated, scalable way to flag AI-generated profile pictures to protect members from inauthentic accounts across a platform serving hundreds of millions of users.

## Approach / System design
LinkedIn collaborated with UC Berkeley professor Hany Farid (via the LinkedIn Scholars program) on lightweight, embedding-based detectors. The core insight: GAN-generated faces have highly regular facial geometry — averaging many synthetic images yields sharp, aligned facial features, whereas averaged real photos show no such regularity. They built two complementary detectors that learn this structural regularity — a PCA-based linear embedding and an autoencoder-based embedding — and compared them against a Fourier-embedding baseline. Models were trained on 100,000 real LinkedIn profile photos plus 41,500 synthetic faces, and evaluated across multiple synthesis engines (StyleGAN1/2/3, Generated.photos, Stable Diffusion) to test cross-engine generalization.

## Key decisions
- Scoped detection to faces/profile photos rather than general synthetic-image forensics, letting simple embeddings exploit GAN facial regularity.
- Set an operating point of 1% false positive rate, prioritizing not misflagging real member photos in production.
- Trained on GAN-generated data but explicitly measured generalization to unseen engines, including diffusion models.
- Chose lightweight PCA/autoencoder embeddings over heavier CNN forensic classifiers.

## Stack
PCA-based linear embedding and autoencoder-based embedding detectors (plus a Fourier baseline); training/evaluation data from StyleGAN1, StyleGAN2, StyleGAN3, Generated.photos, and Stable Diffusion; 100K real LinkedIn photos + 41.5K synthetic faces.

## Results
- 99.6% of synthetic profile photos detected at a 1% false positive rate on real photos.
- Outperformed state-of-the-art CNN-based forensic classifiers from the academic literature.
- Generalization to Stable Diffusion outputs was limited — diffusion imagery lacks the GAN regularities the embeddings exploit.

## Takeaways
Domain-focused, lightweight embedding models can beat complex CNN forensics when the target class (GAN faces) has exploitable structural regularities. Detectors keyed to one generator family degrade on fundamentally different generation processes (diffusion), so coverage must evolve with the threat. Academia–industry partnerships can move research into internet-scale trust-and-safety deployment quickly.
