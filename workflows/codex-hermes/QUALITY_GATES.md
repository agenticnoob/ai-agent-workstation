# Quality Gates

## Gate 0: Scope

Codex can execute without guessing: working directory, allowed files, do-not-touch boundaries, validation commands, and result path are explicit.

## Gate 1: Implementation

Codex followed the task, avoided out-of-scope files, ran requested validation where possible, and recorded failures honestly.

## Gate 2: Validation

Tests/build/lint/typecheck pass, or failures are understood and documented.

## Gate 3: Review

Hermes inspects result files, changed files, git diff, validation output, risks, and missing edge cases.

## Gate 4: Memory hygiene

Only stable, non-sensitive, declarative facts are kept as memory candidates or promoted to Hermes persistent memory.
