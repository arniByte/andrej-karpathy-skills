---
name: plan-first
description: Run BEFORE writing code on any non-trivial task. Surfaces hidden assumptions, lists competing interpretations of an ambiguous request, presents tradeoffs, and produces a short step-by-step plan where each step has a verification check (test-first for bugs). Triggers when asked to add, build, implement, refactor, design, or fix something non-trivial. Also invokable manually as /plan-first. Skip for trivial typo/one-line changes.
license: MIT
---

# Plan First

Run this BEFORE writing code on any non-trivial task. It operationalizes Karpathy Principles 1 (Think Before Coding) and 4 (Goal-Driven Execution): stop coding on silent assumptions, and turn a vague request into verifiable goals.

**Skip for trivial tasks** (typo fixes, obvious one-liners). Use judgment.

## Procedure

Before touching code, produce this short brief:

1. **Restate the goal** in one sentence. If you can't, the request is unclear — ask.

2. **Surface assumptions.** List every assumption you'd otherwise make silently (scope, inputs, file locations, data shape, edge cases). Mark each as `confirmed` or `needs confirmation`.

3. **Check for ambiguity.** If the request has more than one reasonable interpretation, list them — do not pick silently. Ask which one, or state which you'll proceed with and why.

4. **Note tradeoffs / simpler paths.** If a simpler approach exists, say so. If there's a cost/benefit fork, name it.

5. **Write a verifiable plan.** Each step pairs an action with a check:
   ```
   1. [action] → verify: [observable check]
   2. [action] → verify: [observable check]
   ```
   Prefer test-first for bugs and validation: write a failing test that reproduces the issue, then make it pass.

## Output

A short brief, not an essay. If anything is `needs confirmation` or genuinely ambiguous, stop and ask before coding. Otherwise proceed to implement against the plan, looping until each `verify` passes.
