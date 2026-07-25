---
id: cs2346
title: "PurpleLlama: Meta's Open Safety Toolkit for LLMs Including Llama Guard, Prompt Guard, and Code Shield"
company: Meta
primary_category: moderation
sub_category: policy-enforcement
year: 2023
source_url: https://github.com/meta-llama/PurpleLlama
tags: [llm-safety, llama-guard, safety-classifier, prompt-injection, jailbreak-detection, input-output-moderation, open-source]
---

# PurpleLlama: Meta's Open Safety Toolkit for LLMs Including Llama Guard, Prompt Guard, and Code Shield
**Meta** · 2023 · [source](https://github.com/meta-llama/PurpleLlama)

## Problem
Open generative AI models ship without guardrails: applications built on them face unsafe inputs and outputs, prompt injection and jailbreak attempts, insecure code suggestions, and cybersecurity misuse. Meta's Purple Llama project provides tools and evaluations so the community can build responsibly with open models, with safety layered around (not just inside) the model.

## Approach / System design
The project takes a "purple teaming" stance — combining offensive red-team and defensive blue-team perspectives — and splits into safeguards and benchmarks. Safeguards: the Llama Guard series (versions 1–3) are input/output moderation classifiers fine-tuned from Llama models, detecting violations of the MLCommons hazard taxonomy and malicious code, with Llama 3.x-based versions supporting 128k context and multimodal input; Prompt Guard detects prompt injection and jailbreak attempts targeting LLM applications; Code Shield filters insecure code suggestions at runtime, including protection against code interpreter abuse. Benchmarks: CyberSec Eval v1–3 measure cybersecurity safety of LLMs grounded in CWE and MITRE ATT&CK — insecure code suggestion rates and compliance with malicious requests — expanding across versions to code interpreter abuse, offensive capabilities, prompt injection, visual attacks, and spear phishing.

## Key decisions
- Layered, specialized components at input, output, and system levels rather than a single monolithic filter.
- Building classifiers by fine-tuning Llama foundation models rather than training separate architectures from scratch.
- Split licensing: benchmarks under MIT, models under Llama Community licenses, enabling both research and commercial use.
- Integration into the Llama reference system and llama-recipes so safeguards ship alongside the models.

## Stack
Python (majority of the codebase), C++, JavaScript; models fine-tuned on Llama 3.1/3.2 foundations with 128k context and multimodal support; benchmarks based on CWE and MITRE ATT&CK standards.

## Results
Initial CyberSec Eval findings showed meaningful cybersecurity risks for LLMs, both in recommending insecure code and in complying with malicious requests, motivating the safeguard suite. Per the catalog summary, these tools are used to protect Meta AI products in production.

## Takeaways
- Production LLM safety requires layered tooling — detection models plus benchmarks — deployed across input, output, and system levels.
- Standards-grounded evaluations (MLCommons taxonomy, CWE, MITRE ATT&CK) make safety measurable and comparable.
- Open-sourcing safety infrastructure with permissive licensing lets the wider ecosystem adopt the same protections.
