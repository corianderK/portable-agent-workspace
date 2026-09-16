# Handoff protocol

A handoff should be reproducible, auditable, and safe even when the incoming agent has zero access to the outgoing agent's chat history.

## 1. Outgoing agent checkpoint

Before stopping:

- finish or explicitly stop the current atomic step;
- save files;
- run relevant verification;
- update `HANDOFF.md`;
- update machine-readable state when needed;
- persist external IDs/receipts immediately;
- inspect `git status`;
- record blockers and the exact next action.

## 2. Incoming agent recovery

The incoming agent reads:

```text
AGENTS.md
→ ORCHESTRATOR.md
→ HANDOFF.md
→ orchestration/state.json
→ relevant docs / ADRs
→ git status / git log
```

It should then state its reconstructed understanding before acting.

## 3. Read-only validation first

The first handoff to a new harness/model combination should be read-only.

Success criteria:

- correct milestone;
- correct current task;
- correct completed/in-progress work;
- correct blockers and safety gates;
- correct tests/checks;
- correct next action;
- no file modifications.

## 4. Tool compatibility test

Before a full autonomous run, perform a minimal tool-use test such as:

```text
Read AGENTS.md and ORCHESTRATOR.md.
Do not modify files or run commands.
Report the first heading from each file and confirm both were read using tools.
```

This catches model ↔ harness tool-protocol incompatibilities cheaply.

## 5. Controlled execution

For the first real task with a new harness/model:

- allow file reads/searches;
- ask before shell commands;
- ask before edits;
- ask before external network actions;
- protect `.env` and credentials;
- choose a small, reversible step.

## 6. Full handoff

Only increase autonomy after the combination demonstrates:

- reliable tool calls;
- correct scope discipline;
- correct verification behavior;
- correct checkpoint updates.

## 7. Return handoff

When returning to the original agent, do the same recovery process. The original agent should not assume its old conversation is newer than the repository state.