# Recovery Policy

This document defines the first snapshot recovery policy for Agent Human Layer.

See also:

- [Route format](./route-format.md)
- [Risk levels](./risk-levels.md)
- [Release gate policy](./release-gate-policy.md)
- [AHL flow](./ahl-flow.md)

## Core idea

GitHub is audit. Snapshot is recovery.

Git records what changed. A snapshot gives the human a fast way back to a known-good state.

## What a snapshot is

A snapshot is a human-readable save point for restoration.

It exists so a human can return to a known-good state when Git alone is too slow, too risky, or not enough.

## What a snapshot is not

Snapshots are not the same as Git history.
Snapshots are not a replacement for review.
Snapshots are not a replacement for CI.
Snapshots are not a promise that nothing ever breaks.

## Policy

- Actual snapshot contents should usually not be committed to the repository.
- The repository should contain recovery policy, snapshot rules, and restore instructions.
- The repository should not usually contain live backup folders, production data, secrets, machine-specific snapshots, or large generated archives.

## When Git is enough

Git is enough when the work is source-only, the branch is clean, the change is small, no generated files are involved, no local configuration is involved, and no production-adjacent files are involved.

Examples:

- typo fix
- README wording change
- issue template copy edit
- comments only
- documentation-only change

## When a snapshot is required

A snapshot is required when the change touches generated assets, local environment files, production-adjacent configuration, risky or broad changes, or anything where the agent cannot clearly explain what will be restored.

Examples:

- config file
- route format
- risk policy
- generated-facing instruction file
- file that agents rely on
- a directory used by agents or automation

## Recovery levels

### Level 0: No snapshot required

Use when the work is tiny and source-only.

Required explanation:

- identify the branch
- identify the changed file
- explain that Git history is enough

### Level 1: Git recovery

Use when Git is enough.

Required explanation:

- current branch
- starting commit
- changed files
- revert path

### Level 2: File snapshot

Use when a small number of important files are touched.

Required explanation:

- exact files copied
- snapshot location
- restore instruction

### Level 3: Folder snapshot

Use when a directory is risky or multiple related files are touched.

Required explanation:

- exact folder copied
- snapshot location
- restore instruction
- what is intentionally excluded

### Level 4: Stop and ask

Use when the agent cannot safely define recovery.

Required behavior:

- stop before editing
- explain the missing recovery path
- ask for the minimum needed information

Required phrase:

```text
I cannot safely proceed because I do not have a recovery path.
```

## Agent requirements

Before risky work, the agent must show:

```text
Recovery:
- Current branch:
- Starting point:
- Recovery level:
- Save point:
- Snapshot location:
- Restore method:
- What is excluded:
```

If no snapshot is needed, the agent must still say why.

## Example

```text
Risk: Small documentation / instruction work

Intent:
- Create the first instruction-only Skill.
- Do not add scripts yet.

Route:
- Create skills/agent-human-layer/SKILL.md.
- Do not change BELIEF.md.
- Do not change README.md.
- Do not create scripts yet.

Recovery:
- Current branch: issue branch for Skill work
- Starting point: main before the Skill file is added
- Recovery level: Level 1 — Git recovery
- Save point: branch start commit
- Snapshot location: none required
- Restore method: delete the new Skill file or revert the commit
- What is excluded: no generated assets, secrets, database, or production state
```
