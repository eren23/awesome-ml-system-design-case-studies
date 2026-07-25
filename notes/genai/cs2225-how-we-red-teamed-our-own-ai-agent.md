---
id: cs2225
title: How We Red-Teamed Our Own AI Agent
company: Block
primary_category: genai
sub_category: agents
year: 2026
source_url: https://engineering.block.xyz/blog/how-we-red-teamed-our-own-ai-agent-
tags: [red-teaming, ai-safety, agent-security, adversarial-testing]
---

# How We Red-Teamed Our Own AI Agent
**Block** · 2026 · [source](https://engineering.block.xyz/blog/how-we-red-teamed-our-own-ai-agent-)

## Problem
Block wanted to understand how attackers could weaponize goose, their open-source AI agent, to compromise employees. The guiding question: in what ways could attackers leverage goose against Block staff?

## Approach / System design
An internal red-team exercise ("Operation Pale Fire") ran three attack campaigns. Campaign 1 — calendar injection: external calendar invites reach primary calendars without email notifications, so the team hid prompt injections in event descriptions using zero-width Unicode characters, aiming to trigger goose's developer shell into downloading an infostealer payload. Campaign 2 — recipe poisoning: after hitting rate limits, they pivoted to goose's shareable "recipe" workflow packages, embedding injections in base64-encoded recipe URLs with ASCII smuggling and a mock Google Meet for credibility. Campaign 3 — direct social engineering: contacting goose developers under a false pretext (reporting an RTL text bug), which led an employee to run a poisoned recipe and trigger payload delivery. This was the successful path.

## Key decisions
- Attack the agent through the human's real inbox and calendar rather than only the model, testing the whole socio-technical system.
- Use obfuscation (zero-width Unicode, base64, ASCII smuggling) to slip injections past human review.
- Rely on behavioral monitoring to catch atypical activity when prevention fails.

## Stack
Google Calendar API and Meet for pretexting; zero-width Unicode obfuscation; base64-encoded recipe delivery; goose's developer shell and recipe system as the attack surface; behavioral monitoring for detection.

## Results
No formal metrics. The three campaigns ran over roughly five days initially, with about 50 calendar invites sent per day before pivoting away from that channel. Social engineering ultimately succeeded where the automated channels were rate-limited or blocked.

## Takeaways
AI agents differ from traditional software: they mix instructions and data unpredictably and need defense-in-depth, not a single control. Block's mitigations included restricting external calendar-sender visibility, transparent recipe visualization in the UI, stripping zero-width characters, and prompt-injection detection. Human factors dominate — social engineering beat the technical defenses.
