---
name: surgical-review
description: Run BEFORE committing or when reviewing your own pending changes. Audits the working git diff so every changed line traces to the requested task; flags drive-by refactoring, reformatting/style drift, gratuitous comment or docstring edits, unrelated code touched as a side effect, and orphaned imports. Triggers before commits and on requests like 'review my changes' or 'check the diff'. Also invokable manually as /surgical-review.
license: MIT
---

# Surgical Review

Run this BEFORE committing, or when asked to review your own pending changes. It operationalizes Karpathy Principle 3 (Surgical Changes): every changed line should trace directly to the requested task.

## Procedure

1. **Get the diff.** Run `git diff` (and `git diff --staged`) to see every pending change.

2. **Classify each hunk** against the task:
   - **In scope** — directly implements the request. Keep.
   - **Necessary cleanup** — imports/variables/functions YOUR change orphaned. Keep.
   - **Out of scope** — drive-by refactor, renamed variables, reformatting, quote-style changes, added type hints/docstrings, or edits to comments/code the task didn't require. Flag.

3. **Watch for these common side effects:**
   - Reformatting or whitespace churn in untouched code
   - Changed or removed comments you didn't need to touch
   - Style drift (quotes, spacing, type hints) inconsistent with the file
   - Deleting pre-existing dead code that wasn't part of the task
   - Behavior changes smuggled into a "cleanup"

4. **Report.** List in-scope vs out-of-scope changes. For each out-of-scope change, recommend reverting it — or, if it's pre-existing dead code worth removing, mention it rather than deleting silently.

## Output

A short verdict: either "diff is surgical — every change traces to the task," or a list of out-of-scope hunks to revert before committing. Revert the out-of-scope changes (confirm first if behavior is affected), then the diff is ready to commit.
