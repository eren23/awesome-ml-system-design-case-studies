---
id: cs2193
title: Evaluating image segmentation models for background removal for Images
company: Cloudflare
primary_category: cv
sub_category: segmentation
year: 2025
source_url: https://blog.cloudflare.com/background-removal/
tags: [background-removal, dichotomous-segmentation, BiRefNet, IS-Net, SAM, segment-anything, workers-ai, transparent-background]
---

# Evaluating image segmentation models for background removal for Images
**Cloudflare** · 2025 · [source](https://blog.cloudflare.com/background-removal/)

## Problem
Cloudflare Images needed automatic background removal that works across wildly varied inputs — e-commerce product shots to user-generated content — with accuracy on fine boundaries, while fitting the latency and VRAM constraints of production edge infrastructure.

## Approach / System design
The team benchmarked dichotomous image segmentation models using the open-source rembg harness on two datasets: a Humans set (7,000+ people images) and DIS5K (diverse objects/scenes). Candidates: U2-Net (multi-scale global+local analysis, 176 MB), IS-Net (two-step intermediate supervision for cleaner boundaries, 179 MB), BiRefNet (bidirectional refinement passing information between global and local contexts, 973 MB), and Meta's SAM, which was excluded for low unprompted accuracy and high inference time. Models were evaluated on both the 23 GB VRAM production-target GPU and a 94 GB reference GPU, scored with IoU, Dice coefficient, and pixel accuracy. BiRefNet won on quality and now runs via Workers AI inside Cloudflare Images.

## Key decisions
- Weighted IoU and Dice over pixel accuracy, since pixel accuracy is misleading on background-dominant images.
- Preferred general-purpose model variants over specialized ones for broad applicability.
- Accepted BiRefNet's slower inference in exchange for clearly better edge detail and contextual understanding (e.g., correctly isolating wheel spokes and full garments where others failed).
- Served through Workers AI at the edge rather than inside the core Images service.

## Stack
rembg evaluation harness; U2-Net, IS-Net, BiRefNet, SAM candidates; IoU/Dice/pixel-accuracy metrics; Workers AI GPU inference integrated with Cloudflare Images.

## Results
BiRefNet-general: 0.87 average IoU and 0.92 average Dice across both datasets; inference 821ms on the 23 GB GPU vs 351ms on the 94 GB GPU. Comparative averages on the 23 GB GPU: U2-Net 307ms, IS-Net 351ms, BiRefNet 821ms.

## Takeaways
For background removal, boundary quality is the product — a bidirectional global/local architecture that "checks small details against overall structure" justified 2–3x slower inference. Metric choice matters: pixel accuracy flatters models on background-heavy images, so IoU/Dice should drive selection.
