For read-only work, do not load AHL.

Before state-changing work, use the lightest runtime entry:

1. If the handoff contains a **Scope Card** for this exact target and no stop condition has fired, use it. Do **not** reread AHL merely because this is a new agent/session.
2. Otherwise read `skills/agent-human-layer/SKILL.md` once.
3. Do not preload `ahl-flow.md` or policy owners. If a concrete high-consequence question appears, search only the relevant reference section.

AHL is a seatbelt, not a workflow. It must be cheaper than the work it protects.
