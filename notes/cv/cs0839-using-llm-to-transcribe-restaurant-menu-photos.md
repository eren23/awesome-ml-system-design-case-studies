---
id: cs0839
title: Using LLM to transcribe restaurant menu photos
company: Doordash
primary_category: cv
sub_category: image-classification
year: 2025
source_url: https://careersatdoordash.com/blog/doordash-llm-transcribe-menu/
tags: [ops, CV, LLM]
---

# Using LLM to transcribe restaurant menu photos
**Doordash** · 2025 · [source](https://careersatdoordash.com/blog/doordash-llm-transcribe-menu/)

## Problem
DoorDash historically relied on humans to transcribe and update restaurant menus from photos — costly and slow. LLMs can automate this, but real-world menu photos vary widely in structure and quality, so a meaningful fraction of LLM transcriptions are wrong, and naive automation would hurt menu accuracy.

## Approach / System design
A partial-automation pipeline with a guardrail (supervision) layer rather than fully trusting the LLM:
1. Validated menu photos go to a transcription model.
2. A guardrail model scores the predicted quality.
3. High-confidence outputs are auto-accepted and published.
4. Low-confidence outputs are routed to the existing human transcription process.

The transcription side evolved from an OCR → LLM pipeline (OCR extracts raw text, the LLM converts it into structured menu categories/items) to also incorporating multimodal LLMs that read the photo directly and infer structure, run alongside the OCR+LLM path.

## Key decisions
- Invest in a guardrail/supervision layer instead of endless LLM prompt engineering, since directly fixing the LLM across all failure modes would require huge investment.
- Identify three failure categories: inconsistent menu structure, incomplete menus, and low photo quality.
- Guardrail model is a traditional ML classifier using three feature groups: photo features (quality, layout complexity), OCR-output features (ordering consistency, text fragmentation), and LLM-output features (confidence/structural signals).
- The guardrail decouples model choice from the pipeline, letting the team adopt new SOTA models (e.g., multimodal) quickly.

## Stack
OCR; (multimodal) LLMs for transcription; guardrail classifier — compared LightGBM, a ResNet-based net, and a ViT, with LightGBM best (and fastest), reflecting that model complexity should match limited labeled-data availability.

## Results
Human-in-the-loop routing preserved accuracy while capturing automation value on the easy cases. The guardrail framework let DoorDash adopt newly released models quickly. The source (and secondary summaries of it) do not give precise automation-rate or accuracy numbers.

## Takeaways
For high-accuracy automation over messy real-world inputs, a quality guardrail that routes low-confidence cases to humans is often a better investment than chasing a perfect generator. A simple gradient-boosted classifier over photo/OCR/LLM features beat heavier vision models given limited labels.
