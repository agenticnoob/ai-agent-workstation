# SOUL Optimization Review

## What was reviewed

- Existing runtime persona file: `/Users/ai/.hermes/SOUL.md`
- Multi-agent workflow docs under `/Users/ai/agent-workspace/workflows/codex-hermes-openhuman/`

## What changed

The runtime SOUL file was optimized to align Hermes behavior with the Codex + Hermes Agent + OpenHuman workflow.

Key additions:
- explicit Human / Hermes / Codex / OpenHuman role boundaries
- primary workflow path reference
- default workspace directory map
- Markdown artifact flow
- quality gates
- memory gate and OpenHuman promotion rules
- stronger result/review policy
- clearer distinction between temporary task artifacts and durable memory

## Backup

A timestamped backup was created before editing:

- `/Users/ai/.hermes/SOUL.md.bak-20260516-235432`

## Files changed

- `/Users/ai/.hermes/SOUL.md`
- `/Users/ai/agent-workspace/reviews/soul-optimization.md`

## Risks

- This changes future Hermes behavior because `~/.hermes/SOUL.md` is the active persona file.
- The new SOUL is longer and more workflow-specific, but still keeps the same core safety and workspace boundaries.

## Validation

- Re-read the beginning of `/Users/ai/.hermes/SOUL.md` after writing.
- Confirmed backup exists.

## Next steps

- Start a fresh Hermes turn or session and observe whether the updated SOUL produces the desired workflow behavior.
- If it feels too heavy, simplify the Quality Gates and Artifact Flow sections.

## Verdict

APPROVED
