# Governance Sync Rule Review

## Verdict

APPROVED

## Review Summary

Added an explicit governance synchronization rule: SOUL.md, `/Users/ai/agent-workspace` workflow documentation, and `/Users/ai/projects/my-agents-mcp` are a strongly linked set. Any change to one requires checking whether the other two need corresponding updates.

## Files Changed

- `/Users/ai/.hermes/SOUL.md`
- `/Users/ai/agent-workspace/README.md`
- `/Users/ai/agent-workspace/README.zh-CN.md`
- `/Users/ai/agent-workspace/workflows/codex-hermes/README.md`
- `/Users/ai/agent-workspace/workflows/codex-hermes/AGENT_RUNBOOK.md`
- `/Users/ai/agent-workspace/memory/MEMORY_CANDIDATES.md`
- `/Users/ai/projects/my-agents-mcp/README.md`
- `/Users/ai/projects/my-agents-mcp/README.zh-CN.md`
- `/Users/ai/projects/my-agents-mcp/MEMORY_CANDIDATES.md`

## Validation Checked

- Searched SOUL.md, `/Users/ai/agent-workspace`, and `/Users/ai/projects/my-agents-mcp` for existing source-of-truth / synchronization language.
- Confirmed the new rule is now represented in all three areas.
- Confirmed the change is documentation and memory-candidate only; no secrets, credentials, external integrations, or hidden automation were added.

## Memory Hygiene

- The user's preference was promoted to Hermes persistent user memory because it is durable, non-sensitive, and directly affects future workflow behavior.
- A matching stable candidate was staged in workspace/project memory candidate files.

## Risks

- Low. The change adds explicit operational policy and does not alter code execution paths.
- Main risk is verbosity; the rule is intentionally phrased as a check requirement rather than mandatory edits every time.

## Next Steps

- Commit and push the documentation updates in `/Users/ai/agent-workspace` and `/Users/ai/projects/my-agents-mcp`.
