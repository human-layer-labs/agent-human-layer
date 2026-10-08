Before any task that may change code, files, data, configuration, repository state, deployment state, or another real system state, use the lightest AHL entry route:

1. If the current handoff includes a valid AHL Snapshot for this exact Target/scope and no snapshot stop condition has fired, use the Snapshot. Do not reread the full AHL graph merely because this is a new agent or session.
2. Otherwise read skills/agent-human-layer/SKILL.md once. The router decides whether the task qualifies for the Zero-Tax Fast Path or must escalate.
3. Read skills/agent-human-layer/references/ahl-flow.md and owner policies only when the router or a real escalation trigger requires them. Do not preload them as startup ceremony.

Pure explanation or read-only investigation does not require AHL unless the task is moving toward a change.

AHL exists to reduce risk without becoming the work. Optional AHL overhead that costs more than the bounded work it protects is a design failure; remove redundant ceremony before adding more controls.
