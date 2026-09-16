# Read-only handoff test

Use this before allowing a new coding agent to modify the repository.

```text
Read AGENTS.md and follow the repository's documented resume protocol.

This is a cross-agent handoff test.
Do not modify any files and do not execute the next task.

Recover the current project state entirely from the repository and report:
- current milestone
- current batch/task
- completed work
- work currently in progress
- blockers
- safety/execution constraints
- current test status
- exact next action you would take if authorized
- which repository files you used to reconstruct the state
```

A successful handoff should reproduce the same project state the previous agent believed it had, without relying on prior conversation history.