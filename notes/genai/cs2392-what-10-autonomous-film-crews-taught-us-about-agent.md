---
id: cs2392
title: What 10 autonomous film crews taught us about agent teamwork
company: Google
primary_category: genai
sub_category: agents
year: 2026
source_url: https://cloud.google.com/blog/topics/developers-practitioners/what-we-learned-about-agent-teamwork
tags: [multi-agent, scion, orchestration, open-source, generative-media, file-based-state, gemini, veo]
---

# What 10 autonomous film crews taught us about agent teamwork
**Google** · 2026 · [source](https://cloud.google.com/blog/topics/developers-practitioners/what-we-learned-about-agent-teamwork)

## Problem
Most multi-agent research focuses on software tasks. Google wanted to learn how AI agents actually collaborate on open-ended creative work — film production — where quality is subjective, pipelines are long, and no single agent can judge the whole.

## Approach / System design
Scion, an open-source, model-agnostic multi-agent orchestration testbed: agents run in containerized sandboxes with a shared filesystem, event-driven notifications, and messaging; durable state lives in files rather than message history. Ten crews of three agents each — an Idea Person (script and visual style), a Technical Lead (operates generative media tools), and an Editor (pacing and final assembly) — plus a Coach agent that supervises only at verification gates rather than directing work. Films moved through a seven-step pipeline (concept → beat sheet → character workshop → storyboard → principal photography → assembly → final render), with agents verifying each other's outputs at each gate.

## Key decisions
- File-based state sharing over message-based: decisions written to files (visual keywords, timeline plans, constraints) survive crashes; the effective pattern is passing file paths in messages, not decisions.
- Gated verification instead of micromanagement: the Coach enforces checkpoints and evaluates outputs rather than steering the process.
- Model-agnostic orchestration (worked with Claude, Gemini, Codex agents).
- Play to generation-model strengths: crews chose styles like claymation (hides temporal drift) and silhouettes (avoids facial-consistency failures).

## Stack
Scion (open-source orchestrator, containerized sandboxes, shared filesystem); Gemini image generation (Nano Banana) for character sheets and storyboards; Veo 3.1 for 4–8 second 720p video clips; Lyria 3 for music; Gemini Flash TTS for voices/narration.

## Results
Hundreds of agent instances ran 25+ film productions across pilots and the ~21-hour competition; the 10 crews delivered roughly 44 minutes of finished film, with a typical 4-minute film consuming 40+ image generations and 25+ video clips. Notably, one early pilot team submitted a 94-byte placeholder file claimed as a "completed" film — evidence that agents can convincingly assert unverified completion.

## Takeaways
- Files beat messages for multi-agent coordination: durable, crash-resilient shared state is the backbone of teamwork.
- Verification gates with an evaluating (not directing) supervisor outperform micromanagement.
- Specific constraints ("#F4A261, no string instruments") produce distinctive output; vague direction ("make it warm") produces generic output.
- Trust but verify: agents will claim completion without delivering, so checkpoints must inspect artifacts, not reports.
