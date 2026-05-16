# Codex + Hermes Agent + OpenHuman Workflow

This folder defines a practical multi-agent workflow for this local AI agent workstation.

Human-readable summary:
- OpenHuman is the long-term context loop: recall stable context before work, ingest approved durable facts after work.
- Hermes is the operator: plan, coordinate, review, and maintain context hygiene.
- Codex is the implementer: edit repositories, run tests, debug code, and produce result files.

The workflow is intentionally Markdown-first. Agents coordinate through explicit files instead of hidden coupling.

## Why this structure

This setup borrows patterns from popular multi-agent projects and current agent workflows:
- FoundationAgents/MetaGPT: role separation and software-company style workflow.
- openai/openai-agents-python: lightweight handoffs, guardrails, and explicit agent instructions.
- camel-ai/camel: role-playing agents and structured collaboration.
- microsoft/agent-framework: orchestration, state, and workflow boundaries.
- Agent-Field/SWE-AF and similar SWE agent projects: plan → code → test → review → ship loops.
- AGENT-ZERO / deliberate agentic development style repos: auditable Markdown artifacts and human checkpoints.

This workspace adapts those patterns to your local stack:

```text
OpenHuman
   ↓ recall stable user/project/workstation context
Human/User
   ↓ direction / approval
Hermes Agent
   ↓ plans, task files, reviews, context hygiene
Codex CLI
   ↓ implementation, tests, results
Hermes Agent
   ↓ memory candidates from stable facts only
OpenHuman
   ↑ approved durable context ingestion
```

## Folder map

```text
workflows/codex-hermes-openhuman/
├── README.md
├── ARCHITECTURE.md
├── ROLES.md
├── WORKFLOW.md
├── HANDOFF_PROTOCOL.md
├── QUALITY_GATES.md
├── RUNBOOK.md
├── REFERENCES.md
├── templates/
│   ├── OPENHUMAN_CONTEXT.template.md
│   ├── AGENT_CONTEXT.template.md
│   ├── CODEX_TASK.template.md
│   ├── AGENT_RESULT.template.md
│   ├── AGENT_REVIEW.template.md
│   ├── MEMORY_CANDIDATES.template.md
│   ├── OPENHUMAN_INGESTION.template.md
│   └── WORKFLOW_DECISION.template.md
└── examples/
    └── repo-inspection-example.md
```

## Default locations

Use these workspace-level folders:

```text
/Users/ai/agent-workspace/tasks      # concrete task handoffs
/Users/ai/agent-workspace/results    # Codex result reports
/Users/ai/agent-workspace/reviews    # Hermes review reports
/Users/ai/agent-workspace/memory     # memory candidates / ingestion packets
/Users/ai/agent-workspace/workflows  # workflow definitions like this one
```

Project repositories conventionally live under `/Users/ai/projects` unless a task explicitly specifies another path.

## Core rule

OpenHuman participates in the context loop, not in direct code execution.

Use it explicitly in two places:
- before work: recall stable context into `memory/OPENHUMAN_CONTEXT.md` or project-specific context snapshot
- after work: ingest approved durable facts from `memory/*-memory-candidates.md`

Prefer:
- OpenHuman context snapshots before task planning
- Markdown task files
- explicit allowed files
- explicit validation commands
- explicit result files
- explicit review files
- explicit memory candidate files

Avoid:
- vague agent prompts
- unbounded repo edits
- writing temporary progress into OpenHuman or long-term memory
- letting implementation and review happen in the same unverified step
