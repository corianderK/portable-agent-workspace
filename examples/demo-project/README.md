# Demo project

This tiny example shows how the portability files fit together without exposing a real project.

Imagine a project currently at milestone `M2` with task `batch-005` active.

A Codex session stops because its quota is exhausted. Before stopping, it updates:

- `HANDOFF.md`
- `orchestration/state.json`
- Git working-tree state

A developer then opens the **same folder** in another coding harness such as Kilo Code, connects OpenRouter, and runs the read-only handoff prompt.

The incoming agent should reconstruct:

```text
Milestone: M2 integration-validation
Task: batch-005 synthetic-end-to-end-validation
Status: claimed
Tests: passing
Paid data download: blocked pending explicit approval
Next action: reconcile existing claim before external creation
```

Only after that matches the repository evidence should the developer authorize execution.

This example intentionally contains no application code. The pattern is designed to be dropped into an existing repository regardless of language or framework.