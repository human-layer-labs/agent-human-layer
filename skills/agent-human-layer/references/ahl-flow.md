# AHL Flow

AHL should be strict at the boundary, not noisy during exploration.

AHL means Agent Human Layer.
It is the route language for the Skill.

See also:

- [Route format](./route-format.md)
- [Risk levels](./risk-levels.md)
- [Recovery policy](./recovery-policy.md)
- [Release gate policy](./release-gate-policy.md)

## AHL levels

Use these levels:

- `AHL1` = Tiny
- `AHL2` = Small
- `AHL3` = Normal
- `AHL4` = Risky
- `AHL5` = Urgent / production-facing
- `AHL6` = Recovery

## AHL modes

Use these initial modes:

- `AHL Dev`
- `AHL Trial`
- `AHL Release`
- `AHL Hotfix`
- `AHL Recovery`

### AHL Dev

Use during development work.

Policy:

- minimize confirmations
- `AHL1` and `AHL2` may proceed without confirmation if explicitly requested
- `AHL3` may proceed if restore path is clear and work is not production-facing
- `AHL4` or higher requires confirmation
- DB, live data, secrets, production deploy, or unclear restore path requires stop
- report actual AHL level and recovery path after work

Purpose:

```text
Move quickly during exploration without hiding risk escalation.
```

### AHL Trial

Use for snapshot-backed trial.

Policy:

- use in local, dev, staging, or preview
- snapshot restore unit before trial
- allow lighter pre-trial checks when restore is reliable
- failure leads to restore or stop, not endless repair
- not a shortcut for unsafe production release

Purpose:

```text
Try safely because restore is known.
```

### AHL Release

Use when moving toward main or production release.

Policy:

- show release gate
- show affected runtime unit
- show snapshot scope
- show restore method
- show checks to run
- show checks intentionally skipped
- require human confirmation before merge or deploy

Purpose:

```text
Protect the production boundary.
```

### AHL Hotfix

Use for urgent production-facing fixes.

Policy:

- minimal change only
- snapshot first
- one-minute restore required
- relevant checks only
- heavy checks may be skipped only with reason
- no broad refactor
- no infinite repair loop
- if fix fails, restore or stop

Purpose:

```text
Fix urgent pain without losing rollback.
```

### AHL Recovery

Use when restoring.

Policy:

- known-good target required
- restore affected runtime unit
- replacement restore, not overlay
- validate
- do not improve until stable

Purpose:

```text
Get back to safe state first.
```

## Confirmation rules

AHL should reduce human operation, not increase it.

The agent should ask for confirmation only when needed.

### Confirmation is required when

- no AHL level was provided and the work is not obviously AHL1
- agent estimate is higher than requested AHL level
- work is AHL4 or higher
- work targets main or production
- deploy or production release is about to happen
- snapshot scope is unclear
- restore path is unclear
- one-minute restore cannot be named for production-facing work
- DB, live data, secrets, payment data, customer data, or order data may be involved
- conflict appears
- CI repair already failed once and another attempt is needed
- agent wants to change workflow YAML
- work expands beyond the route
- the current request conflicts with the Goal currently being served
- materially different Goal interpretations require different next actions
- the Intent is too unclear to choose a safe next action without inventing it

### Confirmation is not required when

- human explicitly requested AHL1 or AHL2
- agent estimate is equal to or lower than requested level
- work is development-only
- no runtime behavior is affected
- Git recovery is clearly enough
- snapshot creation is a safe extra step and does not change the target system
- the agent is only reporting after completion
- the request differs from the Goal being served but does not conflict with it, and the next action is unchanged
- ambiguity remains, but no material fork in the next safe action is apparent
- the agent is gathering information without committing to a disputed interpretation, and the investigation itself is safe and useful

### Higher requested level is allowed

If the human requests a higher AHL level than the agent estimate, the agent may proceed using the higher safety profile when that does not create harm or unnecessary delay.

Safety can be increased by the human.
Safety cannot be lowered below actual risk.

## First AHL flow

The first AHL flow has five stages:

```text
1. Ask
2. Classify
3. Act
4. Release or return
5. Restore if needed
```

## Stage 1: Ask

The human gives a request.

The human should not need to explain Git, CI, branch protection, snapshot mechanics, or restore commands.

## Stage 2: Classify

Before acting, the agent must identify:

```text
- requested AHL level
- estimated AHL level
- mode
- intent
- affected runtime unit
- route
- snapshot requirement
- restore method
- gate level
- stop conditions
```

If requested level is lower than estimated risk, stop.
If restore path is missing, stop.

The agent must also check whether the Goal behind the request is resolved enough to choose the next action. The Goal does not need to be fully defined.

- Ambiguity remains, but no material fork in the next safe action is apparent -> proceed.
- Reasonable interpretations disagree and would lead to materially different next actions -> ask.
- Intent cannot be resolved enough to choose any safe next action -> ask rather than invent it.

Ask is for the difference needed to choose the next action, not for a complete Goal.

Required phrase:

```text
I cannot safely proceed because I do not have a recovery path.
```

## Stage 3: Act

When evidence arrives during work:

- Belief was wrong -> revise Belief or Route and continue.
- Route was wrong -> revise Route and continue; Route may be revised to serve the Goal, but never to silently cross a declared boundary, stop condition, or required confirmation. A Route change that introduces material new scope or risk returns to Confirmation rules.
- The Goal itself becomes doubtful -> Challenge.
- The human signals a Goal change -> acknowledge it explicitly; never replace the Goal silently.

### In AHL Dev

- stay within route
- stop if risk escalates
- do not touch production
- do not deploy
- report actual AHL level after work

### In AHL Trial

- snapshot restore unit
- run limited trial
- validate
- restore if failed
- do not convert trial into production release

### In AHL Release

- show diff or PR
- show checks
- show skipped checks
- show snapshot scope
- show restore method
- wait for human confirmation before merge or deploy

### In AHL Hotfix

- snapshot first
- make smallest safe change
- run fastest relevant validation
- do not refactor
- do not broaden scope
- restore or stop if fix fails

### In AHL Recovery

- identify known-good snapshot
- move current affected unit aside
- place snapshot at target path
- ensure broken extra files do not remain
- validate
- report restored unit

## Stage 4: Release or return

After development work, the agent should not silently merge or deploy.

For normal development, stop at:

- diff shown
- validation result shown
- commit created
- PR created
- human asked to review

For main or production release, use AHL Release or AHL Hotfix.

Before reporting completion, ask: did the observable result achieve the Goal this work was serving?

- If Goal achievement is observable, report it as achieved, with the evidence.
- If implementation/delivery is complete but achievement depends on external reality the agent cannot observe, report implementation/delivery as complete and Goal achievement as not yet confirmed. Do not guess.
- If evidence shows the Goal was not achieved, do not report completion; return to Belief/Route reconsideration or Challenge instead.

Do not keep working indefinitely because Goal achievement alone remains unconfirmed; report the completed implementation and the open confirmation instead.

Release decision:

```text
- AHL level:
- Mode:
- Target:
- Affected runtime unit:
- Snapshot location:
- Restore method:
- Checks passed:
- Checks skipped:
- Reason skipped checks are acceptable:
- Goal achievement: achieved / not yet confirmed (external) / not achieved
- Stop conditions:
```

## Stage 5: Restore if needed

If the human says:

```text
restore it
```

or:

```text
元に戻して
```

the agent must restore from snapshot when a valid snapshot exists.

Restore is replacement, not overlay.

Expected restore behavior:

1. Identify affected runtime unit.
2. Identify pre-change snapshot.
3. Move current affected unit aside.
4. Place snapshot at target path.
5. Ensure extra broken files do not remain.
6. Validate.
7. Report result.

## Main and production policy

AHL is strict at the main and production boundary.

Before main merge or production deploy, the agent must show:

- what is changing
- why it is safe enough
- what snapshot exists
- how to restore
- what checks ran
- what checks were skipped
- why skipped checks are acceptable
- what should stop the release

The agent must not merge or deploy without explicit human approval unless the repository has a separate trusted automation policy.

## Development policy

Development is allowed to be lighter.

Default behavior:

- `AHL1`: proceed if requested
- `AHL2`: proceed if requested
- `AHL3`: proceed if not production-facing and restore path is clear
- `AHL4+`: stop and confirm

Development must still stop when:

- production is affected
- DB or live state is involved
- secrets are involved
- restore path is unclear
- touched scope expands
- conflict appears

## PR policy

PR creation is allowed because it is reviewable and auditable.

PR creation should include:

- AHL level
- mode
- summary
- files changed
- validation
- snapshot note if applicable
- restore method if applicable
- known skipped checks

The first AHL flow should not automatically merge PRs.

## Merge and deploy policy

Merge and deploy are not ordinary development steps.

Default:

- PR creation: allowed in first AHL flow
- Merge: requires AHL Release confirmation
- Deploy: requires AHL Release or AHL Hotfix confirmation

## Restore-backed trial policy

Use snapshot-backed trial when:

- environment is local, dev, staging, or preview
- affected runtime unit is known
- snapshot exists
- restore method is known
- validation is clear

Do not use it when:

- DB or live state is involved
- production release is hidden inside the trial
- restore target is unclear
- snapshot is missing
- rollback is only theoretical

Required rule:

```text
A snapshot may justify a lighter trial gate, but it does not justify an unsafe production release.
```

## No-loop policy

AHL must prevent CI and conflict loops.

When CI fails:

1. inspect failing check
2. decide whether it relates to changed files
3. if related, make at most one focused repair attempt
4. if unrelated, stop
5. if second run fails, stop

The agent must not:

- keep pushing until green
- fix unrelated checks
- broaden scope
- rewrite workflow YAML to silence failures
- turn a hotfix into a refactor

When conflict appears:

```text
Conflict is a stop condition.
```

## Standard AHL route summary

Before acting, use this format:

```text
AHL Route:
- Requested level:
- Estimated level:
- Mode:
- Intent:
- Target environment:
- Affected runtime unit:
- Files/folders to touch:
- Files/folders to avoid:
- Snapshot required:
- Snapshot scope:
- Restore method:
- Gate level:
- Checks to run:
- Checks to skip:
- Stop conditions:
```

For main or production:

```text
Release confirmation required:
- Merge/deploy target:
- One-minute restore:
- Human approval needed:
```

## Example: development UI change

```text
AHL Route:
- Requested level: AHL2
- Estimated level: AHL2 or AHL3 depending on touched files
- Mode: AHL Dev
- Intent: adjust homepage appearance in development
- Target environment: development
- Affected runtime unit: theme folder if runtime theme files are touched
- Snapshot required: only if runtime folder changes beyond isolated CSS
- Snapshot scope: theme folder if required
- Restore method: Git recovery or folder replacement if snapshot is taken
- Gate level: lightweight development validation
- Stop conditions: production is touched, checkout/order/payment/email/print is touched, scope expands, restore path unclear
```

## Example: main release

```text
AHL Route:
- Requested level: AHL Release
- Estimated level: AHL3
- Mode: AHL Release
- Intent: move dev-confirmed change to main
- Target environment: main / production path
- Affected runtime unit: identified changed runtime folder
- Snapshot required: yes if runtime or production-facing
- Snapshot scope: full restore unit, not changed files only
- Restore method: move current production folder aside and replace it with snapshot
- Gate level: production or relevant release gate
- Checks to run: required release checks
- Checks to skip: only explicitly listed non-relevant checks
- Reason skipped checks are acceptable: snapshot-backed trial in non-production environment
- Stop conditions: snapshot missing, restore method unclear, CI failure unrelated, conflict, DB/live state involved
- Release confirmation required: yes
```

## Example: hotfix

```text
AHL Route:
- Requested level: AHL5
- Estimated level: AHL5
- Mode: AHL Hotfix
- Intent: minimally fix a production-facing button
- Target environment: production
- Affected runtime unit: exact theme or plugin folder
- Snapshot required: yes
- Snapshot scope: full affected runtime unit
- Restore method: replacement restore from pre-hotfix snapshot
- Gate level: urgent production gate
- Checks to run: fastest relevant validation
- Checks to skip: heavy unrelated checks
- Reason skipped checks are acceptable: urgent minimal change with one-minute restore
- Stop conditions: fix touches order/payment/database/auth/email/print, broad refactor needed, restore unclear
- One-minute restore: required
- Release confirmation required: yes
```

## Example: recovery

```text
AHL Route:
- Requested level: AHL6
- Estimated level: AHL6
- Mode: AHL Recovery
- Intent: restore previous known-good state
- Target environment: affected environment
- Affected runtime unit: identify from previous route or human input
- Snapshot required: existing known-good snapshot required
- Snapshot scope: full affected runtime unit
- Restore method: move current unit aside and replace with snapshot
- Gate level: recovery gate
- Checks to run: validation after restore
- Stop conditions: no known-good snapshot, unclear target, DB/live state involved, restore would overwrite unknown human work
```
