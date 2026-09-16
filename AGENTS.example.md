# Universal repository protocol

This file is the first entry point for any AI coding agent working in this repository.

## Resume order

Before making changes:

1. Read `AGENTS.md`.
2. Read `ORCHESTRATOR.md`.
3. Read `HANDOFF.md`.
4. Read `orchestration/state.json`.
5. Read only the product, architecture, ADR, and task documents relevant to the current work.
6. Inspect `git status` and recent `git log`.
7. Identify the currently authorized task and any blockers.

Do not rely on prior chat history as required project state.

## Safety boundaries

- Never expose or commit secrets, API keys, credentials, tokens, private keys, or `.env` files.
- Never repeat an uncertain external creation, purchase, deployment, or other non-idempotent action.
- Never broaden scope without explicit authorization.
- Prefer reversible changes.
- Preserve existing application behavior unless the current task explicitly requires a change.

## Before execution

Confirm:

- current milestone;
- current task;
- acceptance criteria;
- files likely to change;
- tests/checks required;
- actions that require explicit approval.

## Before stopping

Leave the repository resumable:

1. Save working files.
2. Run the relevant tests/checks.
3. Record incomplete work and blockers.
4. Update `HANDOFF.md`.
5. Update `orchestration/state.json` if task state changed.
6. Ensure `git status` accurately reflects unfinished work.
7. Do not leave undocumented partial architectural changes.

A future agent must be able to resume from repository state alone.