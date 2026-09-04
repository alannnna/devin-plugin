---
name: pr-checklist
description: Run Alanna's pre-PR checklist (branch prefix, draft, terse description, test plan, no mixed refactors) before opening or updating a PR
---

Before creating or updating a PR for Alanna, verify each item and fix anything that fails:

1. Branch name starts with `alanna/`.
2. PR will be opened as a **draft**.
3. Description is one terse sentence on *why* the change is needed — no technical walkthrough.
4. Description has a `## Test plan` section. If not, ask Alanna how she is verifying the change (CI existing tests / CI new tests / manual / none-with-reason / TODO) before creating the PR.
5. The diff is additive: no refactors, renames, or moves bundled with new behavior. If there are unexplained deletions, split the refactor into its own PR first.
6. If the PR has already been reviewed, only push commits Alanna explicitly requested or approved.
