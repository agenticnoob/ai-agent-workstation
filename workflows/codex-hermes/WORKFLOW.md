# Workflow

## 1. Local context recall

Hermes reads relevant local memory notes, project context, prior task/result/review files, and repo state when needed.

## 2. Intake

Capture goal, working directory, target repo, constraints, expected deliverable, and risk level.

## 3. Planning

For non-trivial work, Hermes writes a short plan or a bounded Codex handoff.

## 4. Codex handoff

Codex receives exact scope: working directory, allowed files, do-not-touch paths, steps, validation commands, result file, and safety notes.

## 5. Implementation/testing

Codex performs repository edits, tests, builds, debugging, and writes a result report.

## 6. Hermes review

Hermes reviews changed files, git diff, validation output, risks, and next steps.

## 7. Memory hygiene

Hermes extracts only stable, non-sensitive, cross-session facts as memory candidates. Temporary task progress, logs, issue status, PR status, commit hashes, and secrets are excluded.
