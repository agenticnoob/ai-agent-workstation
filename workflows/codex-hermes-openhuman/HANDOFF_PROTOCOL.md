# Handoff Protocol

## Core artifact flow

```text
OPENHUMAN_CONTEXT.md or memory/<project>-openh_context.md
   ↓
AGENT_CONTEXT.md
   ↓
CODEX_TASK.md or tasks/<task>.md
   ↓
AGENT_RESULT.md or results/<task>.md
   ↓
AGENT_REVIEW.md or reviews/<task>.md
   ↓
MEMORY_CANDIDATES.md or memory/<topic>-memory-candidates.md
   ↓
OPENHUMAN_INGESTION.md if approved
```

## Artifact responsibilities

### OPENHUMAN_CONTEXT.md / memory/*-openh_context.md

Purpose:
- stable context recalled before task planning
- user preferences
- workstation conventions
- durable project facts
- do-not-touch boundaries

Owner:
- OpenHuman provides durable facts
- Hermes materializes a task-local snapshot

Must not include:
- secrets
- raw logs
- temporary task status
- unapproved private information

### AGENT_CONTEXT.md

Purpose:
- shared workspace or project context
- current assumptions
- directory map
- active constraints

Owner:
- Hermes

### CODEX_TASK.md / tasks/*.md

Purpose:
- bounded implementation or inspection task for Codex

Owner:
- Hermes

Must include:
- goal
- context
- working directory
- allowed files
- do not touch
- steps
- validation
- expected output
- result file
- safety notes

### AGENT_RESULT.md / results/*.md

Purpose:
- Codex execution report

Owner:
- Codex

Must include:
- summary
- files changed
- commands run
- validation results
- failures
- risks
- follow-up recommendations

### AGENT_REVIEW.md / reviews/*.md

Purpose:
- Hermes review of result and repository state

Owner:
- Hermes

Must include:
- what was done
- what worked
- what failed
- changed files
- risks
- quality gate result
- next steps
- memory candidates

### MEMORY_CANDIDATES.md / memory/*-memory-candidates.md

Purpose:
- stable memory candidates before OpenHuman ingestion

Owner:
- Hermes drafts
- Human approves
- OpenHuman stores if appropriate

Must include:
- declarative candidate fact
- why it is durable
- sensitivity check
- recommended destination
- approval status

Must not include:
- secrets
- short-lived task status
- PR numbers as durable memory
- raw logs unless they describe a stable lesson

### OPENHUMAN_INGESTION.md

Purpose:
- final approved ingestion packet for OpenHuman

Owner:
- Hermes prepares
- Human approves
- OpenHuman ingests

Must include:
- approved facts only
- destination scope: user / workstation / project
- source artifact paths
- ingestion date or pending status

## Naming conventions

Use kebab-case filenames:

```text
tasks/inspect-openhuman-repo.md
results/inspect-openhuman-repo.md
reviews/inspect-openhuman-repo.md
memory/openhuman-workflow-conventions.md
memory/example-project-openh_context.md
memory/example-project-memory-candidates.md
```

## Task status labels

Use simple labels:
- proposed
- ready-for-codex
- running
- blocked
- ready-for-review
- approved
- needs-changes
- memory-pending
- memory-approved
- archived

## Human checkpoint triggers

Pause for human input when:
- credentials are needed
- system-level changes are requested
- destructive commands are needed
- external integration setup is needed
- product direction is ambiguous
- memory contains personal or sensitive information
- OpenHuman ingestion would preserve a new personal/project fact

## Done definition

A task is done only when:
- requested work is complete
- validation passed or failure is explained
- result file exists when Codex ran
- Hermes review exists for non-trivial work
- memory candidates are either written or explicitly not needed
- next step is explicit
