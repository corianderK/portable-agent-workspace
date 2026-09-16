# Lessons learned

## 1. The repository should own the state

The most important portability improvement was not adding another model API. It was moving required project context out of one agent conversation and into normal repository files.

## 2. Git baseline comes before agent switching

Without an initial commit, a new agent cannot reliably distinguish baseline state from unfinished work. Establishing a clean local commit makes cross-agent diffs, rollback, and handoffs much safer.

## 3. Handoff state should be concise

Long-lived design belongs in product/architecture/ADR documents. `HANDOFF.md` should contain only the volatile context a new agent needs right now.

## 4. Start read-only

A new model/harness pair should first prove that it can recover the project correctly before receiving edit or terminal permissions.

## 5. Tool compatibility matters as much as model quality

A strong coding/reasoning model can still be a poor autonomous worker in a particular harness if tool-call parsing is unreliable.

## 6. Cheap models can still be valuable workers

Provider-agnostic repositories make it possible to reserve expensive models for difficult planning/review work and try lower-cost models for routine execution — provided tool reliability is verified first.

## 7. Provider portability is different from harness portability

OpenRouter makes model/provider switching easier, but the coding harness still determines file tools, terminal behavior, approval controls, context handling, and tool-call parsing.

## 8. Controlled autonomy is a useful default

A practical first-run permission policy is:

- Read: allow
- Search/glob/grep: allow
- Shell commands: ask
- Edits: ask
- External directories: ask
- Secrets / `.env`: ask or deny
- Purchases, deploys, live actions: explicit approval only

## 9. External actions need receipts

Any action that cannot safely be repeated — creating remote tasks, deployments, purchases, live transactions — should persist an ID/receipt immediately. A fresh agent should reconcile that marker before retrying.

## 10. The real portability test is returning

A workflow is not fully portable until Agent B can modify/checkpoint the same repo and Agent A can later return, read the updated repository state, and continue without manual re-explanation.
