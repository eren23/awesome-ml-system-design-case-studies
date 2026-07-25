---
id: cs2220
title: Building Ask DoorDash Part Three: Evaluation
company: DoorDash
primary_category: genai
sub_category: chatbots
year: 2025
source_url: https://careersatdoordash.com/blog/building-ask-doordash-part-three-evaluation/
tags: [llm-evaluation, chatbot-eval, automated-testing, customer-support]
---

# Building Ask DoorDash Part Three: Evaluation
**DoorDash** · 2025 · [source](https://careersatdoordash.com/blog/building-ask-doordash-part-three-evaluation/)

## Problem
Early evaluation of the Ask DoorDash agent relied on scattered employee feedback and manual testing, giving limited visibility into quality. The team needed scalable measurement to catch failures systematically before launch.

## Approach / System design
An evaluation harness with four components: (1) Rubric definition — criteria balancing specificity and generalizability across guardrails (communication quality, trust), capability (constraint satisfaction, diversity), and execution (item relevance). (2) Transcript builder — Python scripts that turn raw OpenTelemetry traces stored in ClickHouse into criterion-specific views, removing noise and reassembling evidence scattered across spans. (3) Conversation simulator — an LLM-driven simulated user generates realistic multi-turn conversations from scenarios with fixed tool fixtures for repeatable offline testing. (4) LLM judge — calibrated against human labels using GEPA prompt optimization, scoring each criterion independently with a rationale. The same rubric and judge run on both production sessions and offline simulations.

## Key decisions
- Dual evaluation paths sharing one rubric and judge across production and offline simulation for validity.
- Fixtures freeze external state so results measure agent changes, not environmental drift.
- Criterion-specific evidence scoping — judges see only relevant trace segments — to cut false positives.
- Eligibility gates skip criteria that don't apply to a given session type.

## Stack
OpenTelemetry for instrumentation, ClickHouse for trace storage, GEPA for prompt optimization, an Agent Skills platform; Claude Sonnet 4.6 and Gemini 3.5 Flash tested as base models.

## Results
Monitoring scaled from ~1 employee's feedback to ~2,000 auto-graded sessions per day; regression testing dropped from >6 hours by hand to ~20 minutes; an 8-point quality-score improvement ahead of launch; error rates cut nearly in half; 35% latency reduction from a base-model migration while preserving quality; 11% reduction in reasoning leakage after prompt optimization.

## Takeaways
Measurement alone isn't enough — evaluation has to drive operational improvement loops. Transcript views must match the judgment question, environmental control keeps metrics from measuring confounders, and offline evaluation only transfers if it uses the same rubric and judge as online. Sustaining the infrastructure requires close collaboration with platform teams.
