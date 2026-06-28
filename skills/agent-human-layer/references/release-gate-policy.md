# Release Gate Policy

This document defines the first release gate and snapshot-backed trial policy for Agent Human Layer.

See also:

- [Route format](./route-format.md)
- [Risk levels](./risk-levels.md)
- [Recovery policy](./recovery-policy.md)
- [AHL flow](./ahl-flow.md)

## Core principles

Checks should protect production, not punish progress.

Restore is replacement, not overlay.

## Snapshot scope

Snapshot scope is the restore unit, not merely the changed files.

The agent should snapshot the thing the human expects to be put back exactly.

Examples:

- one important file -> file snapshot
- one plugin -> plugin folder snapshot
- one theme -> theme folder snapshot
- theme plus plugin touched together -> snapshot both runtime folders
- generated assets folder touched -> folder snapshot
- production release artifact changed -> release artifact snapshot

## Risk-based snapshot requirements

### Tiny

- Snapshot usually not required.
- Git recovery is enough.

### Small

- Git recovery is usually enough.
- File snapshot may be used for important or hard-to-recreate files.

### Normal

- Git recovery is enough only when the work is non-runtime and clearly reversible.
- Folder snapshots should be considered for important or directory-level work.
- Normal runtime work should default to folder snapshot unless the agent can clearly justify why Git recovery is enough.

### Risky

- Folder snapshot or release artifact snapshot is usually required.
- Restore method must be known before editing.
- Human confirmation is required before acting.
- If no snapshot or restore path exists, stop.

Required phrase:

```text
I cannot safely proceed because I do not have a recovery path.
```

### Urgent

- Use the smallest safe route.
- Create or identify a snapshot before changing files.
- Define rollback before editing.
- Do not broaden the fix into cleanup.
- Do not run endless repair attempts.
- If the first minimal fix fails, restore or stop.

### Recovery

- Restoration is the goal.
- Do not improve.
- Do not refactor.
- Identify the known-good target.
- Replace the affected runtime unit with the snapshot or target.
- Validate after restore.

## One-minute restore

Production-facing changes should have a restore path that can be executed in about one minute without investigating Git history.

For production-facing work, the agent must show:

```text
One-minute restore:
- Affected runtime unit:
- Snapshot location:
- Restore command or manual restore steps:
- Validation step:
- What is intentionally not restored:
```

## Snapshot-backed trial

A snapshot-backed trial is a controlled route where the team allows lighter pre-trial checks because the affected unit can be restored quickly.

Definition:

```text
Snapshot-backed trial means:
- the affected runtime unit has a pre-change snapshot
- restore method is known
- validation target is clear
- the trial is limited in scope
- failure leads to restore, not endless repair
```

Allowed:

- local development
- dev environment
- staging environment
- preview environment
- feature branch
- non-production test deploy
- production hotfix only with explicit human confirmation and rollback path

Not allowed:

- blind production release
- database migration
- live order data change
- payment data change
- customer data change
- secrets change
- unclear restore path
- broad refactor
- unknown affected runtime unit

Required rule:

```text
A snapshot may justify a lighter trial gate, but it does not justify an unsafe production release.
```

## Production release gates

Production release requires stronger rules than local or staging trial.

For production-facing work, at least one of these must be true:

- required checks pass
- the human explicitly approves an urgent hotfix route
- a one-minute restore path exists and is confirmed

Production release must include:

- affected runtime unit
- risk level
- checks run
- checks intentionally skipped
- reason for skipping
- snapshot location
- restore method
- validation method

## CI gate levels

### Gate 0: No CI needed

Use for:

- issue text
- label description
- planning-only work outside repository files

### Gate 1: Lightweight validation

Use for:

- Markdown
- documentation
- issue templates
- Skill policy documents
- non-runtime references

### Gate 2: Relevant checks

Use for:

- normal source work
- limited configuration work
- scripts
- workflow-related files

### Gate 3: Production gate

Use for:

- production-facing work
- deploy path
- runtime folder change
- order, payment, auth, email, print, database-adjacent behavior
- urgent hotfix

### Gate 4: Recovery gate

Use for:

- restore work
- rollback
- undoing broken agent changes

## Existing YAML policy

Read existing workflow files before proposing CI changes.
Identify current triggers, required checks, deploy workflows, path filters, concurrency rules, and branch protection assumptions before editing YAML.

Actual workflow YAML changes are out of scope unless explicitly requested.

## Avoiding required-check pending hell

Required checks should reliably report a final state.

Heavy jobs may be skipped inside the workflow, but required check names should not remain pending forever.

Recommended direction:

- keep required gate workflow lightweight and always-reporting
- use internal conditions to skip heavy jobs
- separate deploy from PR validation
- avoid making path-filtered workflows required unless their skipped state is safe
- document intentionally skipped checks in the route summary

## PR CI and deploy separation

PR validation and production deploy must be treated as separate concerns.

PR CI should answer:

```text
Is this change safe enough to review and merge?
```

Deploy should answer:

```text
Is this exact merged state safe to release or rollback?
```

## Concurrency policy

For PR validation:

- New commits may cancel older validation runs for the same branch or PR.

For production deploy:

- Deploys should not be casually canceled.
- Deploys should usually run one at a time or require explicit human control.

Do not mix PR cancellation logic with production deploy logic.

## No infinite repair loops

No infinite repair loops.

When CI fails:

1. Identify the failing check.
2. Identify whether the failure is related to the changed files.
3. If related, propose the smallest fix.
4. Apply at most one focused repair attempt unless the human approves another.
5. If unrelated, stop.
6. If the second run fails, stop and report.

Stop message example:

```text
CI is still failing after one focused repair attempt.
I will stop here instead of expanding the scope.
The failing check is:
The likely cause is:
The changed files are:
Recommended next action:
```

## Conflict policy

Conflicts are stop conditions.

When a conflict appears, report:

- conflicted files
- what this branch changed
- what the target branch changed
- whether the conflict is mechanical or semantic
- recommended safe route

For risky or production-facing work, conflict resolution requires human confirmation.

## Database and live state are out of scope

This policy covers:

- file snapshots
- folder snapshots
- release artifact snapshots
- runtime unit replacement
- CI gates
- PR validation
- production release gates

This policy does not cover:

- database rollback
- live order data
- customer data
- payment data
- inventory data
- payroll data
- server secrets
- production environment secrets

Database and live state recovery must be handled in a separate issue with stricter approval.

## Examples

### Docs-only issue

```text
Risk level: tiny
Gate level: Gate 1 — Lightweight validation
Affected runtime unit: none
Snapshot required: no
Snapshot scope: none
Restore method: Git revert
Checks to run: documentation formatting only, if available
Checks skipped: runtime tests and deploy
Reason skipped checks are acceptable: documentation-only change does not affect runtime behavior
Stop conditions: file scope expands beyond the requested document
```

### Normal runtime folder snapshot

```text
Risk level: normal
Gate level: Gate 2 — Relevant checks
Affected runtime unit: wp-content/plugins/example-plugin/
Snapshot required: yes
Snapshot scope: full plugin folder
Snapshot location: pre-change plugin folder snapshot
Restore method: move current plugin folder aside and replace it with snapshot
Checks to run: relevant UI or plugin validation
Checks skipped: unrelated full-suite checks, unless repository policy requires them
Reason skipped checks are acceptable: snapshot-backed trial in non-production environment
Stop conditions: order logic is touched, diff expands, restore path unclear
```

### Risky production-facing example

```text
Risk level: risky
Gate level: Gate 3 — Production gate
Affected runtime unit: checkout plugin or theme unit
Snapshot required: yes
Snapshot scope: full affected runtime folder
Snapshot location: pre-change folder snapshot
Restore method: replace current runtime folder with snapshot
Checks to run: required production-facing checks
Checks skipped: none unless human approves urgent route
Stop conditions: payment/order/email/database behavior is unclear, snapshot fails, validation unavailable
One-minute restore: required
```

### Snapshot-backed trial example

```text
Risk level: normal or risky, depending on touched area
Gate level: Gate 2 for staging trial
Affected runtime unit: selected folder
Snapshot required: yes
Snapshot scope: full restore unit, not changed files only
Snapshot location: pre-trial snapshot
Restore method: move current folder aside and replace with snapshot
Checks to run: minimal staging validation
Checks skipped: full production gate
Reason skipped checks are acceptable: trial is non-production and restore path is known
Stop conditions: restore path unclear, DB/live state involved, production affected
```

### Urgent production hotfix example

```text
Risk level: urgent
Gate level: Gate 3 — Production gate with urgent route
Affected runtime unit: exact production-facing folder
Snapshot required: yes
Snapshot scope: full affected runtime unit
Snapshot location: immediate pre-hotfix snapshot
Restore method: replace affected folder with snapshot
Checks to run: fastest relevant validation
Checks skipped: heavy non-relevant checks
Reason skipped checks are acceptable: urgent route with snapshot and one-minute restore
Stop conditions: fix requires broad refactor, DB/live state involved, rollback unclear
One-minute restore: required before editing
```
