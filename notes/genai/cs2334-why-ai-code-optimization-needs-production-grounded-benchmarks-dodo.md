---
id: cs2334
title: Why AI code optimization needs production-grounded benchmarks (DODO)
company: Datadog
primary_category: genai
sub_category: agents
year: 2026
source_url: https://www.datadoghq.com/blog/ai/production-grounded-code-optimization/
tags: [code-optimization, benchmarking, production-telemetry, llm, agentic-ai, eval]
---

# Why AI code optimization needs production-grounded benchmarks (DODO)
**Datadog** · 2026 · [source](https://www.datadoghq.com/blog/ai/production-grounded-code-optimization/)

## Problem
LLM code-optimization agents that chase synthetic benchmark wins often fail to deliver production gains: benchmarks tuned to synthetic input distributions miss the real workload's characteristics, so agents optimize for the wrong thing — with potentially serious consequences when the "optimized" code ships.

## Approach / System design
DODO (Datadog Observability-Driven Optimizer) grounds optimization in production telemetry using a two-loop agent architecture. Loop 1 generates the benchmark: an LLM agent iteratively writes Go micro-benchmarks, reading CPU profiles from Continuous Profiler for execution shape and capturing real invocations (including receiver object state) via Live Debugger for realistic inputs. Candidate benchmarks are scored against production profiles, with ranked divergences fed back until similarity reaches at least 98%. The benchmark is then frozen. Loop 2 optimizes: a second agent proposes changes to the target function, runs tests and the frozen benchmark, tracks the best version, and iterates until its budget is exhausted. The two agents are decoupled — one may only write the benchmark file, the other only service code — so the optimizer cannot game the score by editing the benchmark.

## Key decisions
- Fuse two production signals: debugger-captured invocations (inputs/state) plus profiler data (CPU execution shape).
- Capture receiver state directly from production instead of reconstructing internal configuration from setup code, which proved brittle.
- Run benchmarks on hardware matching production CPU architecture, with architecture-specific function aliasing and Go runtime frame collapsing.
- Dense feedback: similarity scores plus ranked divergences showing over/under-exercised call paths.
- Freeze the benchmark before optimization begins to prevent reward hacking.

## Stack
Datadog Continuous Profiler, Datadog Live Debugger, Go (target language), LLM agents for benchmark generation and code modification.

## Results
Deployed optimizations cut total service CPU costs by 8%, saving on the order of 10k cores continuously across eight optimized targets. Individual function speedups: intern 40% (9.8% of CPU), FilterPayloads 75% (2.7% of CPU), writeTagsetsMut 76% (2.0% of CPU), filterTags 82% (1.1% of CPU). The equivalent manual effort was estimated at weeks of engineering time.

## Takeaways
- Production grounding surfaces optimizations synthetic benchmarks miss — e.g., one win depended on an observed 25% uppercase ratio in production data.
- Even mature, heavily optimized codebases still hold significant gains.
- Realistic captured state beats synthetic test harness setup.
- Simple agent architectures do well when given dense feedback and clear scoring.
- Production grounding looks like a general principle for AI-assisted development, not just optimization.
