---
id: cs2336
title: Evaluating our AI Guard application to improve quality and control cost
company: Datadog
primary_category: genai
sub_category: eval
year: 2026
source_url: https://www.datadoghq.com/blog/llm-observability-at-datadog-security/
tags: [llm-eval, ai-safety, guardrails, llm-as-a-judge, cost-optimization, prompt-eng, structured-output]
---

# Evaluating our AI Guard application to improve quality and control cost
**Datadog** · 2026 · [source](https://www.datadoghq.com/blog/llm-observability-at-datadog-security/)

## Problem
Datadog's AI agents autonomously investigate alerts, propose code fixes, and review security signals — exposing them to prompt injection, data leaks, and unsafe code execution. AI Guard, the team's in-line guardrail, must evaluate every prompt, model output, and tool call in real time to block unsafe behavior before it reaches downstream systems. The security team needed a rigorous way to measure and improve AI Guard's detection quality while keeping latency and inference costs under control.

## Approach / System design
- **AI Guard placement**: integrated with Datadog's internal AI gateway routing layer, synchronously evaluating every request in-line.
- **Evaluation datasets**: a hybrid of simulated red-team scenarios (prompt injection, indirect data leaks, unsafe execution) and anonymized real agent traces from production traffic, combined to cover edge cases and avoid overfitting to synthetic attacks.
- **Instrumentation**: full tracing through Datadog's own LLM/Agent Observability — capturing prompts, reasoning steps, completions, tool inputs/outputs, latency, and token usage — with the same instrumentation used in development, evaluation, and production so test conditions match reality.
- **Experiments framework**: automated benchmarking of every rule, classifier, or prompt change against the evaluation datasets, tracking accuracy, precision, recall, F1, latency, and token cost, with results linked to PR diffs so each change is measurable and reviewable before deploy.
- **Feedback loop**: production anomalies detected by monitoring are exported back into the evaluation datasets, continuously enriching test coverage.
- **Model strategy**: OpenAI models as primary, custom self-hosted models in the mix, with Claude and Gemini being evaluated for comparison within the same unified pipeline; agentless (API-key) collection was used during early development before full Agent-based collection.

## Key decisions
- Blend simulated attacks with anonymized production traces rather than relying on either alone.
- Reuse one instrumentation layer for debugging, offline evaluation, and production monitoring to eliminate train/serve evaluation drift.
- Gate changes on statistically grounded experiment results tied to PR diffs instead of ad-hoc spot checks.
- Track cost and latency as first-class evaluation metrics alongside quality, using cost analytics to tune evaluation frequency and model selection.
- Keep the pipeline model-agnostic so alternative models can be benchmarked without rebuilding evaluation.

## Stack
Datadog AI Guard, internal AI gateway, Datadog LLM/Agent Observability (trace-level instrumentation), experiments/benchmarking framework, OpenAI models plus custom self-hosted models (Claude and Gemini under evaluation), framework integrations in preparation for LangChain, Pydantic AI, and Mastra; metrics: accuracy, precision, recall, F1, latency, token cost.

## Results
- Building on the existing observability platform saved more than a month of initial development time.
- Trace-level visibility cut investigation of failures from days to minutes.
- The experiments framework provides regression, false-positive, and false-negative measurement across simulated and real datasets for every change.
- Cost analytics informed evaluation frequency and model-selection decisions; specific quality-score or cost-reduction figures are not published in the post.

## Takeaways
- Guardrail products need the same rigor as the systems they protect: versioned datasets, automated experiments, and per-change quality gates.
- Unifying instrumentation across development, evaluation, and production is what makes offline results predictive of live behavior.
- A production-to-dataset feedback loop turns every anomaly into future test coverage.
- Quality, latency, and cost must be optimized jointly — an accurate guardrail that is slow or expensive per-request fails as an in-line component.
