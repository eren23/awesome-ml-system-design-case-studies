---
id: cs2239
title: "The Death of Traditional Testing: Agentic Development and JIT Testing Revival at Meta"
company: Meta
primary_category: genai
sub_category: agents
year: 2026
source_url: https://engineering.fb.com/2026/02/11/developer-tools/the-death-of-traditional-testing-agentic-development-jit-testing-revival/
tags: [jit-testing, ai-testing, agentic-development, code-quality, developer-tools]
---

# The Death of Traditional Testing: Agentic Development and JIT Testing Revival at Meta
**Meta** · 2026 · [source](https://engineering.fb.com/2026/02/11/developer-tools/the-death-of-traditional-testing-agentic-development-jit-testing-revival/)

## Problem
Agentic software development has dramatically accelerated the rate at which code ships, but traditional testing — static test suites that must be manually authored and maintained — cannot keep pace. The maintenance burden and the cost of managing false positives become unsustainable when agents generate code at high volume.

## Approach / System design
Meta's "Catching JiTTest" system generates bespoke tests on demand for each specific code change instead of maintaining a permanent suite. The pipeline: (1) new code arrives in the repository, (2) the system infers the intention of the change, (3) deliberately faulty mutants of the code are created to simulate potential failures, (4) tests are generated and executed against those mutants, (5) rule-based and LLM-based assessors filter results to cut false positives, and (6) engineers receive actionable reports on unexpected behavior changes.

## Key decisions
- On-demand test generation per pull request rather than tests living permanently in the codebase.
- Mutation-based validation: simulated faults via code mutants drive test relevance and prove a test can actually catch a bug.
- LLM-based intent inference of the code change's purpose to minimize false positives.
- Ensemble assessment combining rule-based and LLM assessors so only genuine failure signals reach engineers.

## Stack
Large language models for both test generation and result assessment; mutation-testing tooling for fault simulation.

## Results
No specific metrics are provided in the article.

## Takeaways
The testing question shifts from generic code quality to whether a test finds real faults in a specific change without raising a false positive. This eliminates ongoing test-maintenance cost while keeping bug detection viable at the speed of agentic development.
