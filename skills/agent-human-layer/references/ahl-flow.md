# AHL Flow

AHL should be strict at the boundary, not noisy during exploration.

AHL means Agent Human Layer.
It is the route language for the Skill.

## Route Adherence and safety-critical ordering

This section is the single source of truth for Route Adherence,
safety-critical ordering, and Route revision / violation transitions.
`SKILL.md` and `route-format.md` reference this section and must not create
a separate policy.

### Declaration rule

Every applicable safety-critical ordering constraint must be declared in the
Route before the related state-changing action. It is mandatory; an Agent must
not omit an applicable constraint and thereby bypass Route Adherence.

Examples include:

- branch / savepoint / snapshot before mutation
- required inspect before destructive mutation
- required validation before deploy/release

Normal read-only tool order is not fixed by Route Adherence. Do not create a
total order for ordinary read-only exploration.

### Pre-mutation reachability

When a declared safety-critical ordering constraint exists, immediately before
the related state-changing action ask:

```text
Is this state-changing action currently reachable under the declared safety-critical ordering constraints?
```

If the answer is no, the mutation is prohibited until the prerequisite is
established and the current Route and authorization are valid. Do not apply
this check to every tool or every mutation, and do not create a total order
for actions without an applicable declared constraint.

### Route revision and violation transition

The following are material Route changes:

- removing a safety-critical dependency
- reversing the dependency order
- weakening a prerequisite
- changing the protection target

A material Route change invalidates existing approval and returns to the
ordered Authorization procedure before the state-changing action continues.

A change that preserves the safety-critical dependency itself may, depending on
the circumstances, be a non-material revision. For example, changing snapshot
storage from A to B can remain non-material when the same
`snapshot before edit` dependency is preserved.

For an evidence-driven Route revision:

1. obtain new Evidence
2. update the Route before the mutation
3. re-evaluate authorization when the revision is material
4. perform the mutation only after the current authorization permits it

An explicit human Route change is also a valid revision path; this rule does
not prohibit it.

A Route violation occurs when a state-changing action has already executed
while a safety-critical prerequisite was not established. After a violation:

- stop further mutation
- report the Expected Route
- report the Actual execution
- report the state already changed
- do not create a post-hoc savepoint to retroactively satisfy the Route
- do not rewrite the Route to legitimize the prior mutation
- begin restore or repair only through the existing Authorization procedure

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

## Authorization boundary

Classification and authorization are separate:

- `Requested level` is a safety profile the human explicitly binds to the current work.
- `Estimated level` is exactly one agent classification of consequence.
- `Authorization decision` is either `PROCEED` or `CONFIRM_REQUIRED`.
- A requested or estimated level is not permission by itself.

A level counts as a requested level only when the human explicitly applies it to the current work. A level mentioned in background, an example, quoted policy, prior work, or a report does not count. If the binding is unclear, treat the requested level as unspecified.

The authorization gate covers every state-changing action, including:

- file, data, or configuration mutation
- state-changing shell commands
- commits, pushes, merges, and other repository writes
- deploys and production releases
- state-changing external or API actions
- any other write to an external system

Read-only commands, read-only API calls, and other safe investigation are allowed before authorization. In this policy, `act` means perform a state-changing action; read-only investigation is not an act for the authorization gate.

## AHL modes

Use these initial modes:

- `AHL Dev`
- `AHL Trial`
- `AHL Release`
- `AHL Hotfix`
- `AHL Recovery`

Mode policies describe how to execute only after the ordered authorization procedure returns `PROCEED`. They do not independently grant permission.

### AHL Dev

Use during development work.

Policy:

- apply these permissive mode rules only after the ordered authorization gate returns `PROCEED`
- `AHL1` may proceed when the ordered authorization gate classifies it as AHL1 and returns `PROCEED`, including when no level was specified
- `AHL2` and `AHL3` may proceed only when the ordered authorization gate returns `PROCEED`
- `AHL4` or higher requires a valid bound approval as defined below
- DB, live data, secrets, production deploy, or unclear restore path produces the blocking reason defined below
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
- require valid bound human approval before merge or deploy unless an expressly applicable separate trusted automation policy exists

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

## Authorization blocking rules

This section is the single source of truth for authorization hard stops. Other sections and references provide evidence, prerequisites, or boundary policy; they cannot independently change `CONFIRM_REQUIRED` to `PROCEED`.

AHL should reduce human operation, not increase it. Ask only for what is needed to clear the current blocking reason.

### Blocking-reason classes

Every blocking reason must be reported with its class, current status, and the condition needed to clear it. More than one reason may apply. After a reason is satisfied, keep its identity in the authorization record while distinguishing it from unresolved reasons.

- `APPROVAL_REQUIRED` — a human can satisfy this reason with a valid approval bound to the current authorization scope. Only an expressly applicable separate trusted automation policy may substitute where this policy already allows that exception.
- `PREREQUISITE_REQUIRED` — missing evidence, information, recovery, or another factual safety condition must be supplied or established. Human approval alone cannot satisfy it.
- `BOUNDARY_ROUTE_REQUIRED` — current policy requires a separate route, policy, or stricter approval boundary. Approval of the current route alone cannot satisfy it.

`Proceed`, `OK`, or similar approval language can satisfy only an `APPROVAL_REQUIRED` reason, and only when it unambiguously refers to the current confirmation binding. It cannot create a restore path, supply missing evidence, resolve an unknown prerequisite, or authorize a boundary that current policy does not cover.

### Confirmation binding

A valid human approval must be bound to all of the following as presented to the human:

- the estimated AHL level
- the current Route
- the files and scope
- the target environment
- the full blocking-reason set, including the `APPROVAL_REQUIRED` reason or reasons the approval is intended to satisfy

The agent must record that binding in `Confirmation basis`. A short contextual reply such as `OK` is valid only when it unambiguously approves one currently presented binding and no prerequisite or boundary reason remains unresolved.

Approval expires when the Route, files/scope, target environment, estimated level, or blocking-reason identity or clearance condition materially changes. Marking the same reason satisfied after its named prerequisite is established is a status update, not a material binding change. On the next turn and before every state-changing action after a material change, re-evaluate every hard-stop rule. If approval no longer matches, request confirmation again when required.

### Authoritative hard-stop rules

Use this list when collecting blocking reasons:

| Trigger | Blocking-reason class | Condition needed to clear it |
| --- | --- | --- |
| Estimated level is AHL2–AHL6 | `APPROVAL_REQUIRED` | Valid approval of the presented authorization binding |
| Estimated level is higher than the requested level | `APPROVAL_REQUIRED` | Valid approval bound to the estimated level and current scope |
| Work is AHL4 or higher | `APPROVAL_REQUIRED` | Valid approval bound to the current risky, urgent, or recovery route |
| Work targets main or production | `APPROVAL_REQUIRED` | Valid release or hotfix approval after required release evidence is present, or an expressly applicable separate trusted automation policy |
| Deploy or production release is about to happen | `APPROVAL_REQUIRED` | Valid approval for the exact merge or deploy target, or an expressly applicable separate trusted automation policy |
| Snapshot scope is unclear | `PREREQUISITE_REQUIRED` | Identify the restore unit and snapshot scope |
| Restore path is unclear | `PREREQUISITE_REQUIRED` | Establish a concrete restore method |
| One-minute restore cannot be named for production-facing work | `PREREQUISITE_REQUIRED` | Establish the one-minute restore path |
| Required evidence or another safety prerequisite named by the applicable mode, recovery, or release policy is missing | `PREREQUISITE_REQUIRED` | Establish the named evidence or prerequisite |
| DB, live data, secrets, payment data, customer data, or order data is involved | `BOUNDARY_ROUTE_REQUIRED` | Move to the separate policy, route, and stricter approval required for that boundary |
| Conflict appears | `PREREQUISITE_REQUIRED` | Inspect the conflict and establish the safe conflict route; add bound approval when conflict policy requires it |
| CI repair already failed once and another attempt is needed | `APPROVAL_REQUIRED` | Valid approval for one additional focused attempt |
| The agent wants to change workflow YAML | `APPROVAL_REQUIRED` | Valid approval bound to the exact workflow change |
| Work expands beyond the Route | `APPROVAL_REQUIRED` | Present the updated binding and obtain valid approval |
| The current request conflicts with the Goal currently being served | `PREREQUISITE_REQUIRED` | Resolve the conflict enough to choose the next action |
| Materially different Goal interpretations require different next actions | `PREREQUISITE_REQUIRED` | Resolve the material fork needed for the next action |
| The Intent is too unclear to choose a safe next action without inventing it | `PREREQUISITE_REQUIRED` | Obtain the minimum missing Intent information |

### Permissive rules after `PROCEED`

The following are not independent exceptions. They apply only after the ordered authorization procedure returns `PROCEED`:

- a requested level, when present, is equal to or higher than the estimate
- work is development-only
- no runtime behavior is affected
- Git recovery is clearly enough and no higher-precedence blocking rule applies
- snapshot creation is a safe extra step and is within the authorized scope
- the agent is only reporting after completion
- the request differs from the Goal being served but does not conflict with it, and the next action is unchanged
- ambiguity remains, but no material fork in the next safe action is apparent
- the agent is gathering information without committing to a disputed interpretation, and the investigation itself is safe and useful

### Higher requested level is allowed

If the human explicitly binds a higher requested AHL level to the current work, the agent may use the higher safety profile when that does not create harm or unnecessary delay. This does not by itself grant permission or satisfy another blocking reason.

Safety can be increased by the human.
Safety cannot be lowered below actual risk.

## First AHL flow

The first AHL flow has five stages:

```text
1. Ask
2. Classify and authorize
3. Act
4. Release or return
5. Restore if needed
```

## Stage 1: Ask

The human gives a request.

The human should not need to explain Git, CI, branch protection, snapshot mechanics, or restore commands.

## Stage 2: Classify and authorize

Use this ordered procedure before any state-changing action. Use it again on the turn after `CONFIRM_REQUIRED`, and whenever a material change could invalidate an earlier `PROCEED` or approval.

1. Read the required AHL instructions.
2. Identify the state-changing work the human actually requested, resolve the Goal only enough to choose the next action, and record its actual consequences. A level mention without a request for current work is not authorization. Do not use the `Requested level` to classify consequences. Read-only investigation may continue while gathering the facts needed for later steps.
3. Run the mandatory Classification procedure in [risk-levels.md](./risk-levels.md) using actual consequences. It applies AHL1 exclusions and minimum floors, evaluates remaining consequence dimensions, and returns exactly one `Estimated level`; if unclear, choose the higher level or stop.
4. Resolve the `Requested level` separately, only if the human explicitly bound it to the current work; otherwise record it as unspecified.
5. If the `Requested level` is higher than the `Estimated level`, preserve the estimate and apply the higher requested safety profile separately. Do not copy the requested level into the estimate.

Before step 6, perform the mandatory Goal/scope fidelity check. Compare the human's explicit current mutation scope with the mutation scope the inferred Goal would put into the Route:

- If the inferred Goal would add materially broader mutation scope, surface a separate Goal/scope fork, record an unresolved `PREREQUISITE_REQUIRED`, prohibit mutation until the human chooses the scope, and then re-evaluate the normal ordered Authorization procedure after that choice.
- If it would not, allow Goal-guided Route optimization within the current mutation scope without additional confirmation.

Material scope is not determined by file count alone. Material expansion includes:

- expanding from the requested feature or component to a different component
- expanding to retirement or deletion of an entire subsystem
- adding a data, process, or runtime responsibility
- adding another mutation target that the human did not explicitly request and that is justified only by Goal inference

Non-material changes include:

- changing the implementation method within the same target
- achieving a button-size Goal through hit area or spacing within the same target
- broadening read-only investigation
- adjusting Route details required within the current mutation scope

Evidence-driven investigation may show that broader mutation scope is necessary. Evidence is not permission: surface the broader scope as a Goal/scope fork before mutation, then re-evaluate authorization after the human's choice.

This additional gate applies only to material mutation-scope expansion. It does not add confirmation for read-only exploration, file additions by themselves, AHL1/AHL2 work without material expansion, or same-scope Goal-guided Route optimization.

6. Define the current authorization binding: estimated level, Route, files/scope, and target environment.
7. Collect every applicable reason from the Authoritative hard-stop rules, assign its blocking-reason class and clearance condition, and add the full reason set to the binding.
8. If a prior human approval exists, validate it against the entire current binding.
   - a matching approval may satisfy only its bound `APPROVAL_REQUIRED` reasons
   - approval does not satisfy `PREREQUISITE_REQUIRED` or `BOUNDARY_ROUTE_REQUIRED`
   - any material binding change invalidates the approval
9. Re-evaluate every hard-stop rule using current evidence, including rules that were previously satisfied. Keep an approval-required reason satisfied only while the same valid approval still matches; do not recreate it as an unresolved duplicate merely because its trigger still applies.
10. If any blocking reason remains unresolved, set the final decision to `CONFIRM_REQUIRED`.
11. Only if the human requested the current state-changing work and no blocking reason remains unresolved, set the final decision to `PROCEED`.
12. Permit a state-changing action only when the final decision is explicitly `PROCEED` for that action's current binding.

`CONFIRM_REQUIRED` is monotonic and terminal for the current turn:

- report each blocking reason, its class, and what must clear it
- ask the human only for the required approval, prerequisite, evidence, or boundary route
- do not perform a state-changing action or external write
- end the turn

On the next turn, start from step 1 and re-evaluate all gates. A previous approval is evidence for step 8, not permission to skip the procedure. Later permissive rules such as development-only work, a clear restore path, Git recovery, or “may proceed” cannot change an unresolved `CONFIRM_REQUIRED` back to `PROCEED`.

Before acting, the agent must identify:

```text
- requested AHL level
- estimated AHL level
- authorization decision
- blocking reasons, each with class and clearance condition
- confirmation basis
- mode
- intent
- affected runtime unit
- route
- snapshot requirement
- restore method
- gate level
- stop conditions
```

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
- Route was wrong -> revise Route and continue; Route may be revised to serve the Goal, but never to silently cross a declared boundary, stop condition, or required confirmation. A Route change that introduces material new scope or risk invalidates the prior authorization binding and returns to the ordered authorization procedure.
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
- Requested level:
- Estimated level:
- Authorization decision:
- Blocking reasons:
- Confirmation basis:
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

the agent must first obtain `PROCEED` for the bound recovery action, then restore from snapshot when a valid snapshot exists.

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

- apply every rule below only after the ordered authorization gate returns `PROCEED`
- `AHL1`: may use the unspecified-level fast path only when it satisfies the full tiny-risk policy
- `AHL2`: needs no additional mode-level confirmation after the ordered authorization gate returns `PROCEED`
- `AHL3`: needs no additional mode-level confirmation after the ordered authorization gate returns `PROCEED`, provided the restore path is clear and the work is not production-facing
- `AHL4+`: requires a valid bound approval and resolution of every other blocking reason

Development must still apply every Authoritative hard-stop rule. A development mode rule cannot satisfy or bypass a blocking reason.

## PR policy

PR creation is allowed only after the ordered authorization gate returns `PROCEED` for that exact external write. Reviewability and auditability do not independently grant permission.

PR creation should include:

- estimated AHL level
- authorization decision
- blocking reasons
- confirmation basis
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
- Authorization decision:
- Blocking reasons:
- Confirmation basis:
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
- Estimated level: AHL2
- Authorization decision: PROCEED
- Blocking reasons: none
- Confirmation basis: explicit request for this development UI change at AHL2, bound to this Route, scope, and development target
- Mode: AHL Dev
- Intent: adjust one isolated homepage style in development
- Target environment: development
- Affected runtime unit: one identified theme stylesheet
- Files/folders to touch: the identified stylesheet only
- Files/folders to avoid: all other theme files and production
- Snapshot required: no
- Snapshot scope: none
- Restore method: Git recovery for the one-file change
- Gate level: lightweight development validation
- Stop conditions: production is touched, checkout/order/payment/email/print is touched, scope expands, restore path unclear
```

## Example: main release

```text
AHL Route:
- Requested level: AHL3
- Estimated level: AHL3
- Authorization decision: CONFIRM_REQUIRED
- Blocking reasons: unresolved APPROVAL_REQUIRED — main / production target and exact release; clear with approval bound to this release binding
- Confirmation basis: none; awaiting approval bound to this release Route and exact target
- Mode: AHL Release
- Intent: move dev-confirmed change to main
- Target environment: main / production path
- Affected runtime unit: identified changed runtime folder
- Files/folders to touch: the identified dev-confirmed runtime unit only
- Files/folders to avoid: all unrelated runtime units and DB/live data
- Snapshot required: yes if runtime or production-facing
- Snapshot scope: full restore unit, not changed files only
- Restore method: move current production folder aside and replace it with snapshot
- Gate level: production or relevant release gate
- Checks to run: required release checks
- Ordering constraints:
  - Complete required validation before merge or deploy.
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
- Authorization decision: CONFIRM_REQUIRED
- Blocking reasons: unresolved APPROVAL_REQUIRED — AHL5 and production hotfix; clear with approval bound to this hotfix binding
- Confirmation basis: none; awaiting approval bound to this hotfix Route, scope, and production target
- Mode: AHL Hotfix
- Intent: minimally fix a production-facing button
- Target environment: production
- Affected runtime unit: exact theme or plugin folder
- Files/folders to touch: the exact file required for the minimal fix
- Files/folders to avoid: all unrelated files and DB/live data
- Snapshot required: yes
- Ordering constraints:
  - Create the pre-hotfix snapshot before changing the target.
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
- Authorization decision: CONFIRM_REQUIRED
- Blocking reasons: unresolved APPROVAL_REQUIRED — AHL6 recovery, clear with bound recovery approval; unresolved PREREQUISITE_REQUIRED — identify the known-good snapshot and exact target, clear by establishing both
- Confirmation basis: none; approval cannot be requested until the recovery prerequisite is resolved
- Mode: AHL Recovery
- Intent: restore previous known-good state
- Target environment: affected environment
- Affected runtime unit: identify from previous route or human input
- Files/folders to touch: the exact affected runtime unit after identification
- Files/folders to avoid: all unrelated units and unknown human work
- Snapshot required: existing known-good snapshot required
- Snapshot scope: full affected runtime unit
- Restore method: move current unit aside and replace with snapshot
- Gate level: recovery gate
- Checks to run: validation after restore
- Stop conditions: no known-good snapshot, unclear target, DB/live state involved, restore would overwrite unknown human work
```
