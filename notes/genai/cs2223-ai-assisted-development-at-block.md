---
id: cs2223
title: AI-Assisted Development at Block
company: Block
primary_category: genai
sub_category: copilots
year: 2026
source_url: https://engineering.block.xyz/blog/ai-assisted-development-at-block
tags: [ai-coding, developer-productivity, code-assistant, llm]
---

# AI-Assisted Development at Block
**Block** · 2026 · [source](https://engineering.block.xyz/blog/ai-assisted-development-at-block)

## Problem
Block had to scale AI-assisted development across a heterogeneous organization — mobile, backend, frontend, data, and infrastructure codebases across Square, Cash App, Afterpay, and Tidal — while the AI tooling market was shifting too fast to safely standardize on any single tool.

## Approach / System design
A three-pillar strategy. First, freedom to explore: buy multiple frontier models and tools and let engineers discover what fits their domain instead of standardizing early. Second, an AI Champions program (launched August 2025): 50 developers spending 30% of their time on AI enablement, focused on "repo readiness" — preparing codebases for agent discovery and contribution, gamified as "Repo Quest" with AGENTS.md instruction files, HOWTOAI.md human guides, reusable agent skills, automated AI code review on PRs, and CI/CD integration. Third, structured knowledge transfer: champions teach peers via brownbags, office hours, and demos rather than generic tutorials. For complex work, teams adopted the RPI (Research → Plan → Implement) multi-session methodology: agents research the codebase, document findings, plan in a fresh session, then implement — preventing AI drift.

## Key decisions
- No premature standardization on one AI tool while the landscape is still churning.
- Invest in repo readiness so agents can navigate codebases (AGENTS.md, skills, review bots), tailored per repo type — monorepos vs. services, mobile vs. backend, including a 40,000+ file monorepo.
- Peer champions over top-down training: a colleague's demo lands better than a generic tutorial.
- RPI context-engineering workflow to keep agents on track through complex, multi-step changes.

## Stack
Claude Code, Goose, Cursor, Copilot, Cline, AMP, Firebender; MCP servers; Linear/Jira integration for automated PR generation; an ai-rules automation tool for codebase analysis.

## Results
Within three months of the Champions launch: AI-authored code up 69%, reported time savings up 37%, automated PRs up 21x, and ~95% of engineers regularly using AI for development.

## Takeaways
Repository structure and context scaffolding matter as much as model choice. Champions act as cultural bridges, and well-prepared repos let engineers use agents without constant correction. The next frontier is orchestration — multi-agent parallel workflows — which will need team-specific workshops to close the gap between champions and everyone else.
