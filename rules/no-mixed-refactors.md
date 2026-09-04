---
trigger: model_decision
description: When writing code or opening a PR for Alanna Tempest (alannnna), and the change would restructure, rename, or move existing code alongside new behavior
---

Alanna wants refactors and functionality changes kept in separate PRs. Never bundle them.

- A PR that adds behavior should read as an addition: existing code paths stay byte-for-byte identical wherever possible, and the diff is dominated by new lines rather than moved or rewritten ones.
- If the new behavior genuinely needs the surrounding code restructured first, land the refactor as its own PR *before* the functionality PR, and stack the functionality change on top. Do not do both in one commit or one PR.
- When a diff has unexplained deletions, that is the signal something was refactored that did not need to be. Rework it into an additive shape before asking for review.

Example of what she pushed back on: the Go port of a cadre change (modal-labs/modal#51018) restructured `resolveTemplateValues` — extracting a helper and rewriting the existing single-reference path — to add list-valued secret directives. The equivalent Python PR (#51002) was a clean addition, and she asked for the Go diff to match that shape: keep the existing branch untouched and add a branch for the new case.

## Exception: extracting a small shared util that already-merged code and new callsites both need

She will allow a refactor in the same PR as new functionality when all of these hold:

1. The refactor provably does not change the already-merged behavior it touches — same emitted output (log message text, field names, order, values, formatting), same guard conditions, same thresholds. Verify this explicitly and say in the PR how you convinced yourself.
2. The new callsites justify the extraction (i.e. you are not refactoring speculatively).
3. The refactor is small and obvious — one shared helper, no new package, no exported-signature changes, no restructuring of surrounding functions.

Keep behavior that only one callsite needs *out* of the shared util, since pushing it down would change the merged callsite's behavior. Example: modal-labs/modal#54627 extracted `shadowTokenAge(claims, ttl, leeway, now)` from the merged client-auth shadow-TTL logging in #54758 and reused it for map and attempt tokens; the map/attempt-only leeway and per-`{kind, fcID}` log dedup deliberately stayed at that callsite, and the auth path changed only by routing its arithmetic through the util. Align vocabulary across the callsites when you do this (all three used `shadow*` names) so the file does not read half-migrated.
