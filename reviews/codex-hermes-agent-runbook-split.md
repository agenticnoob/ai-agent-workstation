# Hermes Review: Human Quickstart and Agent Runbook Split

## What was reviewed

- `workflows/codex-hermes/README.md`
- `workflows/codex-hermes/QUICKSTART.zh-CN.md`
- `workflows/codex-hermes/AGENT_RUNBOOK.md`

## What changed

- Clarified that `QUICKSTART.zh-CN.md` is human-facing and not an agent operating procedure.
- Added `AGENT_RUNBOOK.md` as the concise agent-facing execution note for Hermes and Codex task runners.
- Updated `README.md` to point to both:
  - human quickstart: `QUICKSTART.zh-CN.md`
  - agent runbook: `AGENT_RUNBOOK.md`
- Updated the quickstart documentation policy section to reflect this split.

## Rationale

The human quickstart should optimize for the user's future reading and copy/paste usage. Agent execution notes should be shorter, stricter, and avoid forcing agents to parse user-facing explanation. Splitting them keeps both audiences clear without returning to the previous many-document structure.

## Validation checked

- Read back `README.md`, `QUICKSTART.zh-CN.md`, and `AGENT_RUNBOOK.md`.
- Checked local markdown links in the three workflow docs; missing links: none.
- Listed active workflow markdown files.
- Checked git status.

## Risks

- Low. Documentation-only change.
- Adds one agent-facing doc, but avoids recreating the previously removed architecture/roles/workflow/runbook/quality-gate sprawl.

## Required fixes

None.

## Memory candidates

None. This is a documentation structure decision already encoded in the workflow docs.

## Verdict

APPROVED
