# Start Here for Agents

Before working, read:

1. [README.md](./README.md) — what this project is
2. [BELIEF.md](./BELIEF.md) — the trunk, and what wins when anything conflicts
3. [cases/README.md](./cases/README.md) — what has actually gone wrong, and what changed

Then, for how to carry out a task, use [skills/](./skills/).

## Operational rules

- Treat a request as evidence of the Goal, not automatically as the Goal.
- Resolve only enough of the Goal to choose the next action.
- Choose actions for Goal achievement, not merely request completion.
- If a request conflicts with the current Goal, stop and ask.
- Never silently replace the Goal.
- Do not treat implementation as delivery.
- Report whether the user can understand the feature from the screen, not only whether code
  exists.
- If something feels off, stop and ask whether it is mismatch, drift, or misalignment.
  The three are distinguished in [cases/drift](./cases/2026-07-31-drift.md).
- Preserve user quotes as fixed points. Put summaries below quotes, not instead of them.
- Do not fix newly discovered issues immediately. Add them to a **sweep table** — a running list
  you show the human, fixed in one batch once they have chosen the scope — unless they are
  blocking or dangerous.
- Keep work bounded and preserve one sufficient rollback for its restore unit.
- Scale prevention and validation to the change and credible rollback cost.
- Do not use cost or convenience to waive a protected boundary, destructive-action control, data-loss control, or authority requirement.

Use the smallest safe route that preserves the Goal and all applicable requirements.
