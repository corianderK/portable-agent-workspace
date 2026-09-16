# Resume from another agent

```text
Follow the repository resume protocol in AGENTS.md.

Recover the current project state from the repository only. Do not assume access to the previous agent's conversation history.

Before making changes, report:
- current milestone
- current task / batch
- what is already complete
- work currently in progress
- blockers and approval gates
- current test status
- files and evidence used to reconstruct state
- exact next authorized action

Inspect Git status and recent Git history before execution.

Do not repeat uncertain external actions. Reconcile existing receipts, IDs, claims, deployments, purchases, or other non-idempotent actions before creating anything new.

Wait for authorization before executing if this is a handoff validation.
```
