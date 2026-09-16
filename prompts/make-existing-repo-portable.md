# Make an existing repository portable

Copy/paste this into the agent that currently understands your project best.

```text
This is NOT a request to migrate the repo away from the current coding environment, change its filesystem path, or rebuild the multi-agent architecture.

I want to keep using this exact same local repository in my current primary environment.

The goal is only to make the repo safely resumable by other AI coding agents when the current provider or quota is unavailable, so I can open the same folder in another coding environment, continue working, then later return to the original environment and continue again.

Please inspect what already exists first and make the smallest necessary changes.

Requirements:

1. Make the repository the source of truth for project state.
2. Preserve existing product, architecture, ADR, orchestration, and application files.
3. Create or normalize a universal AGENTS.md resume protocol.
4. Create or normalize a provider-neutral ORCHESTRATOR.md.
5. Keep short-lived current execution context in HANDOFF.md.
6. Persist machine-readable state in orchestration/state.json if appropriate.
7. Define a safe checkpoint protocol for quota exhaustion, interruption, or provider failure.
8. Ensure a new agent can recover state without prior chat history.
9. Do not add model APIs to the application unless the product itself requires them.
10. Do not move, duplicate, or migrate the repository.
11. Preserve existing behavior and avoid over-engineering.
12. Before making changes, audit the current repo and propose the smallest portability changes needed.

Validation should include a read-only handoff test from a fresh agent/session.
```
