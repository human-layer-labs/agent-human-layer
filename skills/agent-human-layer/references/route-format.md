# Route Format

This document defines the first human-readable route summary format for Agent Human Layer.
Do not act before showing the route.

See also:

- [Risk levels](./risk-levels.md)
- [Recovery policy](./recovery-policy.md)
- [Release gate policy](./release-gate-policy.md)
- [AHL flow](./ahl-flow.md)

## Required fields

Every route summary must include:

```text
Intent:
Risk:
Route:
Boundaries:
Stop conditions:
Recovery:
```

For larger or riskier tasks, also include:

```text
Assumptions:
Files to touch:
Files to avoid:
Validation:
Open questions:
```

## Field meanings

### Intent

Restate what the human asked for, what success looks like, and what is intentionally not included.

### Risk

Classify the work before acting. Use the current known risk language:

```text
tiny
small
normal
risky
urgent
recovery
```

If the risk level is unclear, say so and choose the higher level or stop.

### Route

Explain where the work starts, what branch or working area is used, what will be changed, what order the work will happen in, and how the work will be reviewed.

### Boundaries

State what the agent will not touch. Boundaries prevent a small request from becoming a hidden rewrite.

### Stop conditions

Define the conditions that require the agent to stop before continuing. Stop conditions are mandatory.

### Recovery

Explain how the work can be undone. Recovery is always required.

## Standard format

Use this shape before acting:

```text
Intent:
- ...

Risk:
- ...

Route:
- ...

Boundaries:
- ...

Stop conditions:
- ...

Recovery:
- ...
```

For bigger tasks:

```text
Intent:
- ...

Assumptions:
- ...

Risk:
- ...

Route:
- ...

Files to touch:
- ...

Files to avoid:
- ...

Boundaries:
- ...

Stop conditions:
- ...

Recovery:
- ...

Validation:
- ...
```

## Rules

- Do not act before showing the route.
- Keep the route proportional to the size and risk of the task.
- Use plain language first.
- State boundaries clearly.
- Never skip stop conditions.
- Never skip recovery.

If no recovery path exists, say:

```text
I cannot safely proceed because I do not have a recovery path.
```

## Example: tiny documentation change

```text
Intent:
- Fix one typo in README.md.

Risk:
- Tiny documentation-only change.

Route:
- Edit README.md only.
- Show the diff.
- Commit the typo fix.

Boundaries:
- Do not change BELIEF.md.
- Do not change examples.
- Do not rewrite surrounding sections.

Stop conditions:
- More than the typo needs changing.
- README structure appears inconsistent.
- The file has unexpected conflict markers.

Recovery:
- Current branch: current working branch
- Starting point: current commit before editing
- Recovery level: Level 1 — Git recovery
- Snapshot location: none required
- Restore method: revert the typo-fix commit
- What is excluded: no generated files, secrets, database, or production state
```

## Example: Skill creation

```text
Intent:
- Create the first instruction-only Agent Human Layer Skill.
- The Skill should define how agents show intent, risk, route, boundaries, stop conditions, and recovery.
- Do not add scripts yet.

Risk:
- Small documentation / instruction work.

Route:
- Create skills/agent-human-layer/SKILL.md.
- Keep the Skill instruction-only.
- Reference BELIEF.md as the trunk.
- Show the diff before committing.

Boundaries:
- Do not change BELIEF.md.
- Do not change README.md unless explicitly requested.
- Do not add scripts.
- Do not create snapshot folders.
- Do not change GitHub issue templates.

Stop conditions:
- The Skill path already exists with conflicting content.
- The scope expands into scripts or restore implementation.
- The route requires changing BELIEF.md.
- No clear recovery path exists.

Recovery:
- Current branch: issue branch for Skill work
- Starting point: branch start commit
- Recovery level: Level 1 — Git recovery
- Snapshot location: none required
- Restore method: delete the new Skill file or revert the commit
- What is excluded: no generated files, secrets, database, or production state
```

## Example: risky folder work

```text
Intent:
- Reorganize the skills folder structure.
- Preserve existing Skill behavior and references.

Risk:
- Risky folder-level work.

Route:
- Inspect the current skills folder.
- Propose the new folder layout before editing.
- Create a folder snapshot before moving files.
- Move files only after the human confirms the route.
- Show the final diff.

Boundaries:
- Do not delete content without confirmation.
- Do not change BELIEF.md.
- Do not rewrite policy documents unless required.
- Do not add scripts unless explicitly requested.

Stop conditions:
- Existing references would break.
- File ownership is unclear.
- The new structure requires changing project direction.
- Snapshot creation is not possible.
- The human has not confirmed the proposed layout.

Recovery:
- Current branch: issue branch for folder reorganization
- Starting point: branch start commit
- Recovery level: Level 3 — Folder snapshot
- Snapshot location: human-readable local snapshot path
- Restore method: restore the previous skills folder from snapshot or revert the commit
- What is excluded: secrets, generated archives, machine-specific files
```
