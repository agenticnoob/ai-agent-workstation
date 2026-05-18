# Remove OpenHuman From Workstation Review

## What changed

The active workstation architecture was simplified from Codex + Hermes + OpenHuman to Hermes + Codex with Hermes built-in memory hygiene.

## Files changed

- `/Users/ai/.hermes/SOUL.md`
- `README.md`
- `README.zh-CN.md`
- `workflows/codex-hermes/*`
- `reviews/remove-openhuman-from-workstation.md`

## Files removed or renamed

- `workflows/codex-hermes-openhuman/` was renamed to `workflows/codex-hermes/`.
- OpenHuman-specific workflow templates were removed.
- OpenHuman-specific memory ingestion staging files were removed from the active workspace.

## Current active workflow

```text
Local context recall → Hermes planning/review → Codex implementation/testing → Hermes review → Hermes memory hygiene
```

## Quality gate status

- Scope gate: PASS — OpenHuman was removed from active workflow paths, role definitions, and startup reminder text.
- Validation gate: PASS — repository search shows no OpenHuman references in active workflow docs, root README files, SOUL.md, or memory docs; only this removal review names the retired component.
- Risk: LOW — changes are documentation/workflow-policy only; no secrets or external integrations touched.

## Verdict

APPROVED
