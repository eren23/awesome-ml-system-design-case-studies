---
id: cs2372
title: Engineering an Invisible AI Medical Scribe
company: Suki
primary_category: audio
sub_category: asr
year: 2024
source_url: https://www.suki.ai/blog/engineering-an-invisible-and-assistive-voice-agent-for-clinicians/
tags: [medical-asr, clinical-voice, dual-asr, speech-recognition, healthcare, ambient-documentation, Go, Python]
---

# Engineering an Invisible AI Medical Scribe
**Suki** · 2024 · [source](https://www.suki.ai/blog/engineering-an-invisible-and-assistive-voice-agent-for-clinicians/)

## Problem
Clinical documentation drives physician burnout, and generic voice-to-text lacks medical-specific accuracy. Context switching between patient care and documentation breaks workflow. The core tension: a slow but highly accurate system frustrates clinicians, while a fast but inaccurate one forces manual corrections — Suki needed both speed and medical accuracy, delivered invisibly inside the clinical workflow.

## Approach / System design
Suki built an "invisible and assistive" voice agent with:
- A **dual-ASR architecture**: separate speech recognition engines for free-form dictation versus voice commands, with wakeword-based audio routing so the two modes don't confuse each other, and a state-transition mechanism that switches between dictation and command modes without explicit user action.
- **Concurrent processing threads**: a syntactic processor handling dictation and a semantic processor handling commands.
- An **EHR integration layer**: a unified interface abstracting Epic, Cerner, Athena, and Elation, with in-memory caching of patient data so commands execute quickly.
- **Context-aware disambiguation**: patient age, specialty, and appointment type help resolve similar-sounding medical terms.
- **Ambient documentation** capabilities powered by large language models.

## Key decisions
- Prioritized real-time, low-latency medical transcription with a domain-tuned ASR over generic engines.
- Split dictation and command recognition into two ASR paths rather than one model doing both.
- Cached patient data in memory to keep command execution fast.
- Committed to never using protected health information for model training.

## Stack
Google Cloud Platform; Go for backend voice-assistant and EHR services; Python for backend processing; custom medical ASR, intent-extraction models, and LLMs for ambient documentation.

## Results
No specific performance metrics or clinical outcomes in the post; it references a separate KLAS report on clinical and financial ROI without detailing numbers.

## Takeaways
Medical voice AI demands domain-tuned models — generic ASR isn't sufficient — and "invisible" UX comes from architecture: dual recognition paths, automatic mode switching, and caching that keeps latency below annoyance thresholds. Deep EHR integration and privacy-first handling of PHI are as load-bearing as the models themselves.
