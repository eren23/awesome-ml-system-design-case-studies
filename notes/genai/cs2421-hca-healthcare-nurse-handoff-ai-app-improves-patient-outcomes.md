---
id: cs2421
title: "HCA Healthcare Nurse Handoff AI App Improves Patient Outcomes"
company: HCA Healthcare
primary_category: genai
sub_category: rag
year: 2025
source_url: https://cloud.google.com/transform/nurse-handoff-ai-chart-app-hca-healthcare-better-patient-outcomes
tags: [rag, healthcare, nurse-handoff, clinical-notes, vertex-ai, patient-safety]
---

# HCA Healthcare Nurse Handoff AI App Improves Patient Outcomes
**HCA Healthcare** · 2025 · [source](https://cloud.google.com/transform/nurse-handoff-ai-chart-app-hca-healthcare-better-patient-outcomes)

## Problem
HCA Healthcare performs approximately 60,000 nurse handoffs per day across 190 hospitals, with each handoff taking around 40 minutes—totaling an estimated 10 million hours of nursing time annually. Handoffs rely heavily on paper-based processes and individual nurse recall, creating inconsistency and risk of information loss during care transitions.

## Approach / System design
HCA built a mobile-first application on Google Cloud generative AI that synthesizes structured EHR data (orders, test results) and unstructured clinical notes into a structured shift-change summary. RAG is used to identify and cite specific passages from the patient record, providing traceability for every generated claim. The UI presents the AI-generated summary alongside the EHR in a dual-panel view with drag-and-drop customizable widgets so nurses can arrange information to match their personal workflow. Nurses participated directly in AI model training through 3–4 iterative feedback cycles run in Innovation Hubs embedded within operating hospitals.

## Key decisions
Nurses were involved as active trainers rather than passive end-users, which drove meaningful improvements in output relevance and reduced irrelevant content across training cycles. RAG with citations was chosen over pure generation to ensure every summary element is traceable back to a source record, which is essential for clinical safety. The rollout began with acute care medical-surgical units before expanding to more complex care settings, reducing risk by validating on narrower use cases first.

## Stack
Google Cloud generative AI foundation models, LLMs fine-tuned with clinical data, RAG pipeline, HIPAA-compliant Google Cloud infrastructure, mobile-first application with customizable widget UI.

## Results
Early pilot results showed 86% of outputs rated as factual and 90% rated as helpful by nursing staff. New graduate nurses were among the most enthusiastic adopters, reporting increased confidence and a greater sense of support during handoffs. The system was planned to pilot across 5 hospitals before a full rollout to approximately 99,000 nurses.

## Takeaways
Embedding engineers directly in clinical environments and making frontline staff co-trainers rather than just testers produced a model that genuinely fits nursing workflows—a process that cannot be replicated by iterating on data alone. In safety-critical healthcare applications, RAG with per-claim citations is a practical requirement rather than an optional feature, as it allows clinicians to verify AI output before acting on it.
