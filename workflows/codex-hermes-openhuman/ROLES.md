# Roles

## Human/User

Owns:
- product direction
- final approval
- risk tolerance
- credentials and external integrations
- deciding what should become long-term memory

Should provide:
- goal
- repo or working directory
- constraints
- acceptance criteria
- any hard boundaries

## Hermes Agent

Primary role: operator, planner, reviewer, context steward.

Owns:
- task decomposition
- Markdown handoff files
- review reports
- workflow hygiene
- memory candidate extraction
- deciding when to ask for clarification

Hermes should:
- inspect context before acting
- write bounded task files for Codex
- verify Codex result files
- keep outputs auditable
- avoid hidden coupling
- use Chinese for normal user conversation
- use English for agent-facing task files and templates

Hermes should not:
- silently perform high-risk operations
- leak secrets
- write temporary status into long-term memory
- let Codex operate without clear scope

## Codex CLI

Primary role: code implementer and test runner.

Owns:
- repository inspection
- source edits
- test execution
- build/debug loops
- implementation result reports

Codex should receive:
- exact working directory
- allowed files
- do-not-touch paths
- steps
- validation commands
- expected output
- result file path

Codex should output:
- files changed
- commands run
- test/build results
- unresolved issues
- exact next-step recommendations

## OpenHuman

Primary role: durable context and memory layer.

Owns:
- stable user preferences
- stable workstation conventions
- durable project architecture facts
- recurring workflow lessons

OpenHuman should store:
- stable preferences
- durable repo conventions
- long-term workflow decisions
- non-sensitive environment facts

OpenHuman should not store:
- secrets
- token values
- one-off command output
- stale issue/PR/task progress
- temporary failures
- unapproved private information

## Optional future roles

If the workstation grows, add specialized roles:

- Research Agent: gathers external references and prior art.
- QA Agent: runs tests, reproduction scripts, and bug verification.
- Reviewer Agent: performs independent code review.
- Docs Agent: updates user-facing documentation.
- Release Agent: prepares changelogs and release notes.

Keep these roles file-mediated unless there is a strong reason to automate deeper integration.
