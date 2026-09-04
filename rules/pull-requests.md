---
trigger: model_decision
description: When creating or updating a pull request for Alanna Tempest (alannnna)
---

1. Always create PRs as **drafts** (set `draft: true` when calling `git_create_pr`). Alanna will mark them as ready for review herself once she's satisfied with the changes.

2. PR descriptions should be high level and extremely terse. Give one sentence that explains what motivated the change or why the change was necessary (e.g. customer issue, reducing duplicate code, etc). Never write paragraphs that explain the technical details of the code, that's what reading the code is for.

3. Before opening or updating a PR, check the PR description for a **test plan** — a section explaining how the changes were or will be verified (e.g. "Relying on CI tests", "Manually tested by …", "Added new unit tests in …", "No testing needed because …").

If no test plan is present, **do not create the PR yet**. Instead, prompt Alanna with a question like:

> Your PR description doesn't include a test plan. How are you verifying these changes?
> - CI tests (existing tests cover this)
> - CI tests (added new tests)
> - Manual testing (describe what you did/will do)
> - No testing needed (explain why)
> - TODO (edit PR description later)
> - Other

Once she responds, add a "## Test plan" section to the PR body with her answer, then proceed to create/update the PR.
