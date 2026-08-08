---
id: cs1818
title: "Gong — Introducing Gecko: An Open-Source Tool for Annotating Conversations"
company: Gong
primary_category: audio
sub_category: asr
year: "2021"
source_url: https://medium.com/gong-tech-blog/introducing-gecko-an-open-source-solution-for-effective-annotation-of-conversations-2ecec0909941
tags: [diarization, transcription, annotation, segmentation, tooling]
---

# Gong — Introducing Gecko: An Open-Source Tool for Annotating Conversations
**Gong** · 2021 · [source](https://medium.com/gong-tech-blog/introducing-gecko-an-open-source-solution-for-effective-annotation-of-conversations-2ecec0909941)

## Problem
Building high-quality training data for speaker diarization and transcription requires annotators to play back audio, segment speakers, and correct model outputs — tasks that existing generic tools handled poorly. Gong needed an annotation workflow that combined media playback, segmentation editing, and model comparison in one place.

## Approach / System design
Gecko is a serverless web application that embeds an audio/video player alongside a segment-level annotation interface, so annotators can make corrections while listening without switching contexts. The tool also supports loading and comparing the outputs of multiple ASR and diarization models side by side, allowing annotators to use model hypotheses as starting points and correct only the errors.

## Key decisions
Building serverless kept deployment friction low and made the tool easy to host without dedicated infrastructure. Open-sourcing Gecko allowed the broader research community to benefit from the same annotation workflow Gong uses internally. Supporting multi-model comparison directly in the interface addresses the practical need to evaluate system improvements against labeled ground truth.

## Stack
Serverless web architecture; browser-based media playback; open-source release.

## Results
Not covered in the source.

## Takeaways
Annotation tooling is a critical but often underinvested component of the ASR development pipeline. Integrating playback, editing, and model comparison into a single interface measurably reduces annotator context-switching and improves label consistency.
