# Checkpoint before exit

Use this when an agent is about to stop because of quota exhaustion, interruption, provider failure, or an intentional handoff.

```text
Checkpoint the current repository state now. Do not start new work.

Before stopping:
- save all intended working files;
- run only the relevant safe verification checks;
- record what completed and what remains unfinished;
- record blockers, failing tests, and pending approvals;
- update HANDOFF.md;
- update orchestration/state.json if execution state changed;
- record any external receipt / task / deployment / purchase ID immediately;
- inspect git status and make the working-tree state explicit;
- do not leave undocumented partial architectural changes.

The next agent must be able to resume safely using repository state only.
```
