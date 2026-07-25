---
id: cs2227
title: 3 Principles for Designing Agent Skills
company: Block
primary_category: genai
sub_category: agents
year: 2026
source_url: https://engineering.block.xyz/blog/3-principles-for-designing-agent-skills
tags: [agent-design, tool-use, agentic-ai, skill-design]
---

# 3 Principles for Designing Agent Skills
**Block** · 2026 · [source](https://engineering.block.xyz/blog/3-principles-for-designing-agent-skills)

## Problem
Tribal knowledge — undocumented processes, runbooks, style guides — has always been poorly captured, and AI agents can't use knowledge that isn't structured. Block needed a way to package this knowledge so agents can discover and execute it reliably.

## Approach / System design
Block built an internal Skills marketplace with 100+ skills organized into role-specific bundles (frontend, Android, iOS). A skill is a folder-based repository: a SKILL.md instruction file plus supporting assets (scripts, templates, MCP servers). The format is an open standard that works across Claude Code, Goose, Cursor, Amp, GitHub Copilot, and Gemini CLI. Design follows three principles plus one bonus pattern.

## Key decisions
- Principle 1 — deterministic execution: lock down anything that must be consistent. The Repo Readiness skill scores repos via a bash script with fixed point values and binary pass/fail, not agent judgment, so every run yields identical results.
- Principle 2 — agent reasoning where it helps: reserve LLM judgment for interpretation, novel content generation, and contextual conversation, since every repo and every conversation is different.
- Principle 3 — constitutional constraints: write explicit rules into the skill doc (e.g., never override or recalculate a script-produced score) to stop agents from "helpfully" improvising around the workflow.
- Bonus — design for a conversational arc: skill outputs should feed follow-up actions (diagnosis → treatment) across multi-turn interactions.

## Stack
Markdown skill files, bash scripts with JSON output, version control; consumable by Claude Code, Goose, Cursor, Amp, GitHub Copilot, and Gemini CLI.

## Results
No quantitative adoption or time-savings metrics are given in the post.

## Takeaways
Skills turn documentation from a read-only artifact into an executable workflow. The craft is drawing the line correctly: scripts for what must be deterministic, agent reasoning for what benefits from judgment, and constitutional guardrails to keep the LLM's variability from breaking the workflow.
