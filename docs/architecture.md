# Architecture

Portable Agent Workspace separates **project state** from **the agent currently operating on it**.

## Principle

The repository is persistent. Agents are disposable.

```text
same local repository
        │
        ├── project docs
        ├── execution state
        ├── Git history
        └── safety / handoff protocol

        ↓ opened by

Codex / Kilo / Cline / Claude Code / future harness
        ↓
model provider
        ↓
GPT / Claude / DeepSeek / Gemini / Kimi / local model
```

## Long-lived state

Long-lived truth belongs in normal repository documentation:

- product requirements;
- architecture;
- ADRs / decisions;
- acceptance criteria;
- stable safety boundaries.

## Short-lived state

Short-lived execution context belongs in `HANDOFF.md` and optionally `orchestration/state.json`:

- current milestone;
- current task;
- active claim / receipt;
- blockers;
- current verification state;
- exact next action.

## Git's role

Git provides:

- a known-good baseline;
- a record of which agent changed what;
- rollback;
- a way for a fresh agent to distinguish committed state from unfinished work.

For this reason, establish a clean local baseline before doing cross-agent execution handoffs.

## Harness vs model

A coding-agent **harness** is the layer that gives a model tools and executes its actions. Examples include Codex, Cline, Kilo Code, and Claude Code.

The harness typically handles:

- file reads/writes;
- repository search;
- terminal commands;
- Git operations;
- browser/MCP tools;
- tool-call parsing;
- approval policy;
- context management.

A capable model may behave differently across harnesses because tool protocols and parsers differ.

## Portability levels

### Level 1 — Read-only recovery
A fresh agent can reconstruct the current project state without prior conversation history.

### Level 2 — Controlled execution
A fresh agent can perform a small reversible task while reads/searches are automatic and edits/commands require approval.

### Level 3 — Full operational handoff
A fresh agent can safely continue the current milestone, verify results, update state, and checkpoint for the next agent.

Validate these levels incrementally rather than granting full autonomy immediately.