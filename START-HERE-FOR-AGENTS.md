# Start Here for Agents

For ordinary execution, **do not preload the AHL repository**.

- Read-only work: load no AHL.
- State-changing work: use [AHL Micro](./skills/agent-human-layer/SKILL.md) once, or use the exact Scope Card already handed to you.
- Child agents with a valid Scope Card do not reread AHL.
- README, BELIEF, cases, the canonical architecture, and `references/` are design/research material. Read them only when the task is specifically about AHL design, research, audit, or a concrete high-consequence semantic question.

The repository must not charge every Agent the cost of understanding how AHL was invented before it can do ordinary work.

## Operational rules

- Treat a request as evidence of the Goal, not automatically as the Goal.
- Resolve only enough of the Goal to choose the next action.
- Choose actions for Goal achievement, not merely request completion.
- If a request appears to conflict with the current Goal, inspect the smallest fact that can resolve the conflict. Ask only when a real Human-owned material choice remains.
- Never silently replace the Goal.
- Do not treat implementation as delivery.
- Report whether the user can understand the feature from the screen, not only whether code
  exists.
- If something feels off, inspect the smallest discriminating fact. Do not stop merely because something is unexpected; stop only when the next safe action depends on unresolved target, authority, protected consequence, or a Human-owned material choice.
- Preserve user quotes as fixed points. Put summaries below quotes, not instead of them.
- If a newly discovered issue is required to finish the current Goal and remains inside the existing scope/authority, fix it and continue. If it is unrelated, separate it. Do not create tracking paperwork unless it is useful for a real follow-up.
- Keep work bounded and preserve one sufficient rollback for its restore unit.
- Scale prevention and validation to the change and credible rollback cost.
- Do not use cost or convenience to waive a protected boundary, destructive-action control, data-loss control, or authority requirement.

Use the smallest safe route that preserves the Goal and all applicable requirements. For execution, use [AHL Micro](./skills/agent-human-layer/SKILL.md); do not preload the reference graph.
