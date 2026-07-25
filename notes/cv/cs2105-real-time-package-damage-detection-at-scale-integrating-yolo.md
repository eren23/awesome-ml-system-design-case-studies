---
id: cs2105
title: "Real-Time Package Damage Detection at Scale: Integrating YOLO in Warehouse Operations"
company: Wayfair
primary_category: cv
sub_category: object-detection
year: 2026
source_url: https://www.aboutwayfair.com/careers/tech-blog/real-time-package-damage-detection-at-scale-integrating-yolo-in-warehouse-operations
tags: [object-detection, yolo, warehouse, damage-detection, quality-control, real-time]
---

# Real-Time Package Damage Detection at Scale: Integrating YOLO in Warehouse Operations
**Wayfair** · 2026 · [source](https://www.aboutwayfair.com/careers/tech-blog/real-time-package-damage-detection-at-scale-integrating-yolo-in-warehouse-operations)

## Problem
Manually spotting damaged packages on warehouse conveyor lines doesn't scale and is error-prone. Damaged shipments that slip through cause customer frustration, replacement delays, and extra logistics cost — Wayfair wanted to catch damage automatically before packages leave the warehouse.

## Approach / System design
Tarragon is a YOLO-based computer vision system integrated into the warehouse sorting flow. High-speed scan tunnels photograph each package in grayscale from six angles (top, bottom, and sides) as it moves along the conveyor. The system must evaluate all images and emit a divert decision in under one second to keep line throughput; flagged packages are diverted to a "Jackpot" lane for manual review and re-boxing. Instead of edge inference at every sorter (hard to scale globally), the model is hosted centrally on Google Vertex AI — cloud round-trip adds ~250ms but stays inside the 1-second SLA and enables centralized 24/7 operation. To build training data cheaply, Wayfair fine-tuned Gemini 2.0 Flash as a classifier to pre-select likely-damaged images from unlabeled data before human annotation. Damage is bucketed into two actionable classes: minor cosmetic (scale 0–2) vs. actionable damage like punctures, tears, and crushing (scale 3–4).

## Key decisions
- YOLO for inference efficiency under a hard real-time SLA.
- Cloud-hosted inference over per-site edge deployment — accept ~250ms latency to gain operational simplicity and global scalability.
- GenAI-assisted labeling (fine-tuned Gemini 2.0 Flash) to slash manual annotation burden on rare-positive data.
- Two-class actionable taxonomy rather than fine-grained damage grades; 20% of training data double-annotated for validation (annotators disagreed 16% of the time), 80% single-labeled for volume.
- Validate at one facility (Erlanger, KY) before network-wide rollout.

## Stack
YOLO object detection; Google Vertex AI model hosting; Gemini 2.0 Flash (fine-tuned) for dataset curation; high-speed six-angle grayscale scan tunnels; conveyor divert integration ("Jackpot" review lane).

## Results
- Model performs over 12x better than the no-skill baseline (baseline accuracy 3.3%, i.e., random guessing on the rare-damage class).
- Met the sub-1-second end-to-end decision SLA including ~250ms cloud inference latency.
- Found diminishing returns past a certain training-data volume — more data stopped helping.
- Successfully validated at the Erlanger, KY sortation facility ahead of network-wide scaling.

## Takeaways
- Real-world CV deployments are as much mechanical engineering as ML: months of camera-calibration work with hardware vendors was critical.
- Cloud inference can beat edge for scaled warehouse CV when the latency budget allows — centralization simplifies everything.
- LLM/VLM-assisted pre-labeling is a force multiplier for building rare-event detection datasets.
- Annotator disagreement (16%) is a useful honesty signal about task difficulty and a ceiling on label quality.
