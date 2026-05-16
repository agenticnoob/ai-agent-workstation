# References and Prior Art

This workflow is inspired by common patterns in well-known multi-agent and agentic software engineering projects.

## GitHub lookup snapshot

A local GitHub API lookup during creation surfaced these popular projects and star counts at lookup time:

| Project | Stars at lookup | Relevant pattern |
|---|---:|---|
| FoundationAgents/MetaGPT | 68011 | role-based multi-agent software company workflow |
| openai/openai-agents-python | 26349 | lightweight agent workflows, handoffs, guardrails |
| camel-ai/camel | 16968 | role-playing agents and multi-agent collaboration |
| raga-ai-hub/RagaAI-Catalyst | 16162 | agent observability, tracing, monitoring |
| microsoft/agent-framework | 10478 | orchestration and multi-agent workflow framework |
| InternLM/MindSearch | 6856 | multi-agent search and synthesis |
| codefuse-ai/codefuse-chatbot | 1289 | SDLC assistant with multi-agent/devops tooling |
| study8677/antigravity-workspace-template | 1219 | multi-agent workspace template for Claude Code, Codex CLI, Cursor, Windsurf |
| MagicCube/agentara | 412 | local personal assistant with Claude Code, Codex, memory, skills, scheduling |
| Agent-Field/SWE-AF | 776 | autonomous software engineering fleet for PRs |
| msitarzewski/AGENT-ZERO | 207 | auditable architecture-first AI-assisted development workflow |
| jmagly/aiwg | 132 | multi-platform AI-augmented software development workflow |
| Matt-Hulme/deliberate-agentic-development | 27 | structured plan-build-ship workflow with checkpoints |

## Patterns adapted here

### Role separation

From MetaGPT/CAMEL-like systems:
- planner
- implementer
- reviewer
- memory/context keeper

Local adaptation:
- Hermes = planner/reviewer/operator
- Codex = implementer/test runner
- OpenHuman = durable memory/context

### Explicit handoffs

From OpenAI Agents-style handoffs and local agent workflow repos:
- agents should exchange clear instructions
- handoffs should include guardrails
- results should be inspectable

Local adaptation:
- Markdown files are the handoff protocol.

### Observability

From RagaAI Catalyst and SWE agent workflows:
- record what happened
- track commands and outputs
- review after implementation

Local adaptation:
- `AGENT_RESULT.md` and `AGENT_REVIEW.md` are the minimum observability layer.

### Human checkpoints

From deliberate agentic development workflows:
- not every step should be fully autonomous
- risky operations require human approval

Local adaptation:
- secrets, destructive commands, external integrations, and product decisions require human input.

## What this workflow intentionally does not copy

It does not require:
- a heavy service mesh
- a database-backed orchestration framework
- automatic cloud agents
- hidden memory writes
- always-on background services

The default is local, inspectable, and Markdown-first.
