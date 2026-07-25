---
id: cs2218
title: Reducing Fraud Loss With an Automated Dynamic Policy
company: Coinbase
primary_category: fraud
sub_category: payment-fraud
year: 2026
source_url: https://www.coinbase.com/blog/reducing-fraud-loss-with-an-automated-dynamic-policy
tags: [dynamic-policy, automated-rules, backtesting, real-time-ml, risk-management]
---

# Reducing Fraud Loss With an Automated Dynamic Policy
**Coinbase** · 2026 · [source](https://www.coinbase.com/blog/reducing-fraud-loss-with-an-automated-dynamic-policy)

## Problem
Traditional fraud controls at Coinbase relied on manually tuned static thresholds that go stale as fraud patterns and operating conditions shift, demand constant human intervention, and ignore dynamic constraints such as limited human review capacity. Static rules also can't adapt when the queue of protective actions (e.g., detailed account reviews) is saturated.

## Approach / System design
Coinbase reframed fraud prevention as a dynamic optimization problem under constraints, built on a reinforcement-learning-style policy framework. A state vector (transaction value, risk scores, system-load metrics) maps to a menu of actions ranging from allow to block, some of which consume constrained resources like manual review slots. A loss function aggregates direct fraud losses, negative user-experience costs, false-positive opportunity costs, and operational expense. A PID-inspired controller dynamically adjusts a budget threshold based on real-time resource utilization: constrained actions are only chosen when their loss advantage exceeds the threshold, which rises with load — preventing queue overflow at peak while maximizing protective actions when capacity is free.

## Key decisions
- Replace human-tuned static thresholds with a policy that optimizes a unified loss covering fraud loss, UX friction, false positives, and ops cost.
- Treat review capacity as a first-class constraint and manage it with PID-style feedback control instead of fixed rate limits.
- Validate via simulation/backtesting against the static-threshold baseline before rollout.

## Stack
Not covered in the source beyond the modeling framework — an RL-based policy layer with a PID-inspired budget controller; specific infrastructure and tooling are not named.

## Results
In simulation, the dynamic policy delivered a significant improvement over the static-threshold baseline with considerable reduction in total expected loss. The static baseline violated the resource constraint (exceeding a 20-actions-per-hour review limit), while the dynamic policy stayed compliant while still optimizing risk mitigation.

## Takeaways
Moving from human-tuned rules to adaptive, constraint-aware automation makes fraud defense both more effective and operationally sustainable. Encoding resource budgets directly into the policy (rather than as afterthought rate limits) is the key design idea, and the pattern generalizes to any resource-constrained decisioning problem beyond fraud.
