# Risk Levels

This document defines the first risk classification policy for Agent Human Layer.

See also:

- [Route format](./route-format.md)
- [Recovery policy](./recovery-policy.md)
- [Release gate policy](./release-gate-policy.md)
- [AHL flow](./ahl-flow.md)

## Levels

Use these levels:

```text
tiny
small
normal
risky
urgent
recovery
```

Choose one level before acting. If the level is unclear, choose the higher risk level or stop and ask.

Risk is based on consequence, not effort.
AI confidence is not proof of safety.

## Rules

- A change can be easy to implement and still be risky.
- Unknown risk must be escalated.
- Recovery must match risk.
- The route must match risk.
- Higher risk requires stronger recovery.

If the agent cannot tell whether a change affects production, data, payment, orders, authentication, email, printing, or generated assets, it must escalate risk.

## Mandatory classification procedure

This document is the single source of truth for Classification. `ahl-flow.md`
calls this procedure before the Authorization binding; it does not redefine
these classification rules.

Apply Classification in this order before any state-changing action:

1. Identify actual consequences without using the `Requested level`.
2. Apply hard eligibility exclusions and minimum floors:
   - the AHL1 four-condition eligibility gate
   - runtime behavior or user-visible runtime output/presentation excludes AHL1
   - database schema or migration changes have a minimum AHL4 floor
   - apply any other explicit floor already present in this policy
3. Evaluate the remaining consequence dimensions using the existing risk levels.
4. Choose exactly one `Estimated level`. If it is unclear, choose the higher
   level or stop and ask.
5. Separately resolve the `Requested level`.
6. If `Requested level` is higher than `Estimated level`, preserve the
   `Estimated level` and apply the higher requested safety profile separately.
7. Pass both levels into the existing Authorization procedure.

The `Requested level` must not be used to calculate the `Estimated level` in
steps 1–4.

### AHL1 eligibility and minimum floors

AHL1 is eligible only when all four conditions are explicitly true:

- one file
- documentation/metadata-only
- no runtime behavior
- no data/config/deploy impact

If any condition is false or unknown, AHL1 is prohibited.

Runtime behavior or user-visible runtime output/presentation affected means the
work is AHL1-ineligible. This includes JavaScript runtime logic and
HTML/CSS user-visible runtime UI or presentation. Runtime exclusion does not
automatically choose AHL2, AHL3, or AHL4; assess the actual consequence using
the remaining levels. A small non-production runtime or source change may be
AHL2 when its actual consequence supports that level.

Adding, changing, or deleting an actual database schema definition or a
database migration has a minimum classification of AHL4 / risky. This
classification floor is separate from Authorization's
`BOUNDARY_ROUTE_REQUIRED`; after Classification, the existing Authorization
procedure must evaluate the database boundary separately.

Risk is consequence, not effort. A one-line change, one-file
change, easy task, quick change, easy review, easy Git recovery, or clear
restore path does not lower Classification or override a hard exclusion or
minimum floor. Difficult, uncertain, or slow recovery may increase the
Estimated level when the existing taxonomy treats recovery difficulty as a
consequence-amplifying factor.

## tiny

Use `tiny` when the work is narrow, source-only, easy to review, and easy to revert.

Typical examples:

- typo fix
- Markdown wording change
- issue template copy edit
- label description change
- README sentence edit
- comments-only change

Allowed scope:

- one file
- documentation or metadata only
- no runtime behavior
- no production path
- no generated assets
- no secrets
- no database
- no deployment configuration

Recovery expectation:

- Git recovery is enough.
- No snapshot is usually required.

## small

Use `small` when the work is limited and reviewable, but it creates or changes real project behavior, structure, or agent instructions.

Typical examples:

- one new documentation file
- one instruction-only Skill file
- one reference policy document
- one GitHub issue template
- one isolated route format
- small non-production source change

Allowed scope:

- one or a few related files
- documentation
- agent instruction files
- isolated non-production source files
- GitHub metadata

Recovery expectation:

- Git recovery is usually enough.
- A file snapshot may be required if the file is important, generated-facing, or hard to recreate.

## normal

Use `normal` when the work is expected development work with meaningful behavior, structure, or workflow impact.

Typical examples:

- add a new reference document and update the Skill to link it
- reorganize a small section of project structure
- modify non-critical scripts
- update validation rules
- change CI configuration in a limited way
- implement a small feature with tests

Allowed scope:

- several related files
- one project area
- non-critical scripts
- documentation plus source
- tests or validation files

Recovery expectation:

- Git recovery is enough only if the work is non-runtime and clearly reversible.
- Folder snapshots should be considered for important or directory-level work.

## risky

Use `risky` when the work could break important behavior, affect production-adjacent systems, or be hard to restore quickly.

Typical examples:

- change payment logic
- change checkout or order confirmation
- change authentication or permissions
- change database schema
- change production deployment workflow
- change generated assets
- reorganize a folder used by agents or automation
- modify restore or snapshot scripts
- change multiple related systems at once

Recovery expectation:

- folder snapshot or release artifact snapshot is usually required
- Git history alone is not enough unless the agent clearly explains why

Required phrase:

```text
I cannot safely proceed because I do not have a recovery path.
```

## urgent

Use `urgent` when the human is asking for a fast fix because something is currently painful, broken, or production-facing.

Urgent does not mean careless. It means the route should be minimal, visible, and reversible.

Typical examples:

- production button is hard to press
- checkout is blocked
- order confirmation is broken
- email sending is failing
- a visible page is broken
- a deployment broke a critical flow

Recovery expectation:

- a fast rollback path is required
- the agent should prefer the smallest safe change
- a hotfix branch is preferred
- a clear before/after diff is required

## recovery

Use `recovery` when the main goal is to restore a known-good state, undo damage, or make the system safe again.

Recovery work is not normal development. Restoration comes first.

Typical examples:

- revert a broken change
- restore a folder from snapshot
- recover a deleted file
- undo an unsafe agent edit
- return production to the last known-good state
- inspect what changed before attempting repair

Recovery expectation:

- identify the known-good target before acting
- replace the affected runtime unit with the snapshot or target
- validate after restore
- do not improve until stable

## Escalation rules

Escalate risk when any of these are true:

- more files are touched than expected
- unrelated files appear in the diff
- the work crosses project boundaries
- runtime behavior changes
- production behavior changes
- data, database, auth, payment, order, print, or email is involved
- deployment or CI behavior changes
- generated files are involved
- scripts are added or changed
- restore path is unclear
- the human's request is urgent
- the agent is unsure

## Example summaries

### tiny

```text
Risk:
- Level: tiny
- Reason: documentation-only typo fix in one file.
- Recovery: Git recovery is enough.
- Escalation trigger: if the change becomes a rewrite or touches other files.
```

### small

```text
Risk:
- Level: small
- Reason: creates one instruction-only Skill file and does not affect runtime behavior.
- Recovery: Git recovery is enough.
- Escalation trigger: if the work requires scripts, README changes, BELIEF changes, or folder reorganization.
```

### normal

```text
Risk:
- Level: normal
- Reason: updates multiple related agent instruction files.
- Recovery: Git recovery is likely enough if the branch is clean.
- Escalation trigger: if route rules conflict with existing recovery policy or require reorganizing references.
```

### risky

```text
Risk:
- Level: risky
- Reason: changes folder structure used by agents and may break references.
- Recovery: folder snapshot required before moving files.
- Escalation trigger: stop if references, ownership, or restore path are unclear.
```

### urgent

```text
Risk:
- Level: urgent
- Reason: production-facing pain with a request for minimal change.
- Recovery: fast rollback path required before editing.
- Escalation trigger: stop if the fix requires broad refactoring or touches order/payment logic.
```

### recovery

```text
Risk:
- Level: recovery
- Reason: the goal is restoration, not new development.
- Recovery: identify the known-good commit or snapshot before acting.
- Escalation trigger: stop if the known-good state is unclear.
```
