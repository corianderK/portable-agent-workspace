# Provider-neutral orchestration

The repository owns the workflow. The model provider does not.

## Orchestrator responsibilities

The orchestrator should:

- recover state from repository files;
- identify the next authorized task;
- avoid duplicate external actions;
- assign or perform work using the currently available coding agent;
- verify results against explicit acceptance criteria;
- persist state before stopping.

The orchestrator may run in Codex, Cline, Kilo Code, Claude Code, another IDE agent, or a future harness. The protocol should not depend on one vendor.

## State machine

```text
recover
→ reconcile existing work
→ identify authorized task
→ plan
→ execute
→ verify
→ record evidence
→ update state
→ checkpoint
```

## Idempotency rule

For any external or non-idempotent action:

1. search for an existing receipt / task ID / claim marker;
2. if uncertain, stop and reconcile;
3. never create a duplicate merely because the current agent cannot see the prior chat;
4. persist the returned identifier immediately after a successful creation.

## Verification

A task is not complete because an agent says it is complete. Completion requires repository-visible evidence such as:

- passing tests;
- expected files/diffs;
- generated evidence/report files;
- acceptance checks;
- recorded external receipts when relevant.

## Provider switching

Provider or harness switching must not change project semantics.

Example:

```text
Codex quota exhausted
→ checkpoint
→ open same repo in Kilo/Cline/Claude Code
→ recover from AGENTS/HANDOFF/state/Git
→ continue
→ checkpoint
→ return to Codex later
```

## Stop conditions

Stop and ask for approval when work would:

- expand scope;
- spend money;
- download/purchase new data;
- deploy to production;
- access secrets;
- perform live transactions;
- delete or irreversibly overwrite important data;
- repeat an uncertain external action.