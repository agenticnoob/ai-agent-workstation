# Quality Gates

Quality gates make multi-agent work auditable and prevent silent drift.

## Gate 0: Scope gate

Before Codex starts, Hermes checks:
- Is the working directory explicit?
- Are allowed files explicit?
- Are do-not-touch boundaries explicit?
- Are validation commands listed?
- Is the result file path explicit?

Pass condition:
- Codex can execute without guessing.

## Gate 1: Implementation gate

Codex checks:
- Did it follow the task?
- Did it avoid out-of-scope files?
- Did it run the requested validation?
- Did it record failures honestly?

Pass condition:
- Result file contains enough detail for Hermes to review.

## Gate 2: Validation gate

Hermes or Codex checks:
- tests pass, or failure is understood
- build passes, or failure is understood
- lint/typecheck pass if relevant
- no accidental secret exposure

Pass condition:
- The change is technically verified or clearly blocked.

## Gate 3: Review gate

Hermes checks:
- spec compliance
- changed files
- git diff where applicable
- risk level
- missing edge cases
- memory candidates

Pass condition:
- review says approved or needs-changes with concrete fixes.

## Gate 4: Memory gate

Hermes checks:
- Is the lesson stable for more than a week?
- Is it non-sensitive?
- Is it useful across sessions?
- Is it a fact, not an imperative instruction?

Pass condition:
- Memory candidate is safe to pass to OpenHuman or persistent memory.

## Escalation rules

Escalate to the human if:
- the task requires credentials
- validation requires external paid services
- destructive operations are proposed
- repo ownership or license is unclear
- agent outputs conflict
- a decision changes product behavior

## Abort rules

Abort or stop the current task if:
- Codex wants to modify files outside scope
- secrets appear in output
- tests reveal broad unrelated breakage
- the task is too vague to validate
- the requested command is destructive and unapproved
