# NEWBORN AHL ATOMIC CUTOVER PLAN — NON-LIVE PLANNING ARTIFACT

Status: `PHASE 7 PLAN — CUTOVER BLOCKED; NO CUTOVER PERFORMED`

Architecture authority: `AHL-CANONICAL-TARGET.md` only.

This plan is derived from the repository state inspected on the
`newborn/implementation` branch at Phase 6. It defines a future Phase 8
mutation route. It does not activate newborn AHL, change runtime files, delete
legacy files, or grant authority for cutover.

## 1. Current live graph inventory

The current live graph was verified against
`4af6316b704fa5235778f92512f74dfc9f27ffa0`. Each current live file below has
the same content hash as that known-good legacy commit.

### Entry and router

1. `AGENTS.md` is the host/project entry instruction. It requires reading the
   live `skills/agent-human-layer/SKILL.md` and live
   `skills/agent-human-layer/references/ahl-flow.md` before mutation. It is
   not itself a policy owner and is retained.
2. `skills/agent-human-layer/SKILL.md` is the live Human-facing entry Skill
   and router. It directs agents into the legacy AHL flow and references the
   legacy supporting policies.
3. `skills/agent-human-layer/references/ahl-flow.md` is the live lifecycle,
   route, target, authorization-hard-stop, recovery, release, and completion
   flow. Its current blocking vocabulary includes the legacy
   `BOUNDARY_ROUTE_REQUIRED` path.

No other host bootstrap file, service, daemon, executable router, or CI entry
mechanism was found in the bounded repository inventory. The future cutover
therefore requires an operator-controlled admission barrier at the Agent/host
execution boundary; it must not invent a new repository service.

### Current live normative owners

| Live path | Current role | Newborn replacement or disposition |
|---|---|---|
| `skills/agent-human-layer/SKILL.md` | Legacy activation, Human-facing route, and hard-stop presentation | Replace in place with staged thin router. |
| `skills/agent-human-layer/references/ahl-flow.md` | Legacy lifecycle, Route Adherence, Target, authorization procedure, blocker table, Recovery/Release placement, and completion flow | Replace in place with staged flow. |
| `skills/agent-human-layer/references/risk-levels.md` | Legacy risk names, AHL1–AHL6 presentation, classification, DB minimum floor, and escalation | Replace with newborn consequence owner; remove after validation and reference audit. |
| `skills/agent-human-layer/references/route-format.md` | Legacy route-summary shape and route presentation | Replace with staged flow/Work Unit semantics; remove after validation and reference audit. |
| `skills/agent-human-layer/references/recovery-policy.md` | Legacy snapshot/recovery levels and restore assumptions | Replace in place with staged Recovery owner. |
| `skills/agent-human-layer/references/release-gate-policy.md` | Legacy snapshot-backed trial, release, CI, and production gate | Replace in place with staged Release owner. |

### Live owner gaps

The following canonical newborn owners have no current live destination:

- `consequence-policy.md`
- `authorization-policy.md`
- `boundary-policy.md`
- `work-unit-format.md`

The current live graph therefore cannot be treated as a partial newborn graph.
No cutover may expose any of these files before the complete coherent graph is
ready behind the admission barrier.

### Valid non-superseded files

- `AGENTS.md` remains the host/project entry floor and is not changed by this
  plan.
- `AHL-CANONICAL-TARGET.md` remains the sole architecture SSoT.
- `newborn-staging/migration/*` and `newborn-staging/sentinels/*` remain
  non-runtime audit evidence.

### Current DB/production, Release, and Recovery paths

- DB/schema work currently receives a legacy minimum AHL4 floor in
  `risk-levels.md` and a legacy `BOUNDARY_ROUTE_REQUIRED` path in
  `ahl-flow.md`.
- Production/release work currently depends on live release-gate policy,
  explicit approval, snapshot/restore expectations, and production checks.
- Recovery currently depends on the live snapshot policy and replacement
  restore instructions.
- The staged newborn Boundary policy is present, but it contains only a
  provider-independent generic adapter model. No concrete DB Boundary
  adapter/path exists in the repository and no live routing currently invokes
  it.

## 2. Newborn activation manifest

The future activation must prepare and switch every row as one logical
transition. Existing destinations are not safe to expose one at a time.

| SOURCE | DESTINATION | ACTION |
|---|---|---|
| `newborn-staging/skills/agent-human-layer/SKILL.md` | `skills/agent-human-layer/SKILL.md` | replace |
| `newborn-staging/skills/agent-human-layer/references/ahl-flow.md` | `skills/agent-human-layer/references/ahl-flow.md` | replace |
| `newborn-staging/skills/agent-human-layer/references/consequence-policy.md` | `skills/agent-human-layer/references/consequence-policy.md` | create |
| `newborn-staging/skills/agent-human-layer/references/authorization-policy.md` | `skills/agent-human-layer/references/authorization-policy.md` | create |
| `newborn-staging/skills/agent-human-layer/references/recovery-policy.md` | `skills/agent-human-layer/references/recovery-policy.md` | replace |
| `newborn-staging/skills/agent-human-layer/references/boundary-policy.md` | `skills/agent-human-layer/references/boundary-policy.md` | create |
| `newborn-staging/skills/agent-human-layer/references/release-gate-policy.md` | `skills/agent-human-layer/references/release-gate-policy.md` | replace |
| `newborn-staging/skills/agent-human-layer/references/work-unit-format.md` | `skills/agent-human-layer/references/work-unit-format.md` | create |

`AGENTS.md` is not a replacement destination and must remain unchanged. It
continues to point to the canonical live paths; the live paths themselves
must resolve to the complete newborn graph after the switch.

## 3. Legacy retirement manifest

The following identifies what becomes obsolete and the earliest safe deletion
or replacement point. No row is actionable during Phase 7.

| Current legacy path/content | Newborn protection | Sentinel basis | Earliest safe point |
|---|---|---|---|
| Live `SKILL.md` content | Thin activation/router and Human compression | S001, S025–S027, S043, S050 | After complete router validation and no legacy fallback reference. Replace in place; do not retain old router content. |
| Live `ahl-flow.md` content | Lifecycle, Target, Route, Evidence, Core, policy loading, failure, and Reality collision | S011–S012, S025, S028–S032, S036–S046, S051 | After all activation checks pass. Replace in place; no old flow remains reachable. |
| Live `risk-levels.md` | `consequence-policy.md` plus flow placement | S001–S006, S048–S050, S054 | Only after newborn consequence and DB Boundary validation pass and a reference scan finds no required legacy consumer. This is blocked now. |
| Live `route-format.md` | `ahl-flow.md` Route semantics and `work-unit-format.md` when durable representation is required | S008, S011–S012, S025–S028 | After live flow/router validation and no direct live reference remains. |
| Live `recovery-policy.md` content | Newborn Recovery Capability, Evidence, applicability, composition, and failure | S014–S020, S024, S053 | After newborn Recovery path validation. Replace in place; do not run old snapshot semantics in parallel. |
| Live `release-gate-policy.md` content | Newborn artifact-to-Target release transition and temporal validation | S034–S035, S040–S041 | After newborn Release path validation. Replace in place; no old release owner remains reachable. |
| No live authorization policy file | Newborn closed-world grant/membership owner | S007–S011, S019–S027, S029–S033, S050–S053, S055 | Create as part of the atomic activation set. |
| No live Boundary policy file | Newborn Boundary owner and concrete DB adapter/path | S041, S049, S051 | Create and validate before retiring the legacy DB/production floor. This is the current cutover blocker. |
| No live consequence policy file | Newborn factual Level owner | S001–S006, S048–S050, S054–S055 | Create as part of the atomic activation set. |
| No live Work Unit format file | Newborn serialization-only owner | S008, S019–S021, S026, S053 | Create as part of the atomic activation set. |

Legacy approval state is not a deletion candidate that can be silently
converted. It is state, not a file: the default is quiescence and fresh
newborn authorization. Any unavoidable carry follows Section 5.

## 4. Mixed-graph prohibition and router switch

The forbidden states are:

- legacy router plus any newborn owner;
- newborn router plus any legacy normative owner; or
- staged runtime copies treated as live authority after activation.

The future cutover must use this logical switch:

1. Prepare all eight source-to-destination replacements/creations without
   changing the live entry path.
2. Establish the admission barrier and hold it through replacement and
   validation.
3. Replace/create all eight live destinations as one contiguous operation.
4. Validate that the live `SKILL.md` resolves only the live newborn owner
   paths, not `newborn-staging/*` and not superseded legacy owners.
5. Release the barrier only after the complete newborn graph and all required
   activation checks pass.

Filesystem writes may not be literally atomic across eight files. The
operator-controlled admission barrier is therefore mandatory: no
AHL-controlled state-changing occurrence may dispatch while the live files
are in a transient mixed state. This is a bounded execution barrier, not a
new daemon, service, or dual-mode runtime.

## 5. Quiescence gate

The objective gate is explicit:

```text
QUIESCENT =
  no new legacy-governed state-changing admission
  AND every in-flight occurrence is settled or conservatively accounted for
  AND no unknown allowance/reservation state is reset
  AND the admission barrier remains held through graph validation
```

The future operator must record `QUIESCENT` or `NOT_QUIESCENT` from observable
facts. `QUIESCENT` requires:

- new legacy-governed state-changing work is fenced at the Agent/host entry;
- in-flight occurrences are enumerated within the available execution
  context;
- known results are settled or explicitly handed to the applicable owner;
- unknown results retain consumed allowance/reservation/occurrence state;
- timeout is not treated as no effect or completion; and
- no operation is broadened merely to finish the cutover.

Read-only inspection may continue during the barrier when it cannot mutate
Human state or dispatch work. If any condition is not established, the gate is
`NOT_QUIESCENT` and activation stops.

## 6. Authority, occurrence, and carry rule

Preferred route: carry **no legacy approvals**. Quiesce legacy work, settle or
conservatively account for occurrences, then begin newborn operation with a
fresh attributable newborn grant.

Carry is permitted only for an unavoidable already-bounded obligation when
all of these are reconstructable exactly:

- original attributable Human or mandate provenance;
- exact scope;
- exact Target and material effects;
- Operation;
- remaining allowance and occurrence/reservation state; and
- policy-basis identity needed to interpret the authority.

Any carried authority is narrowed to the exact obligation, at most an
exact/singleton newborn Envelope. If any field cannot be reconstructed, the
old approval is not carried and a new attributable grant is required. Legacy
numeric AHL5/AHL6, requested caution, or Agent summary never substitutes for
that grant.

Unknown-result state remains consumed/conservative until read-only Evidence
establishes no effect. Reservation state is not reset. Retry requires real
idempotency under the newborn authorization owner.

## 7. Mandatory DB Boundary prerequisite

This plan remains **CUTOVER_BLOCKED** because the Human-owned DB/production
Boundary policy has now been supplied and implemented in the staged adapter,
but independent validation and live activation proof are still pending.

Before any legacy DB/production floor is removed, the future route must first
provide and validate all of the following under the newborn graph:

1. the newborn DB Boundary adapter is activated;
2. the live newborn `SKILL.md`/`ahl-flow.md` route DB-relevant work to it;
3. live validation establishes factual DB/production applicability, exact
   Target, resource, and material effect;
4. live validation recognizes attributable authority explicitly covering that
   exact protected DB target/effect; and
5. live validation proves Boundary result consumption by Authorization and
   local `BOUNDARY_REQUIRED` failure when exact authority is absent.

Only after those five facts are validated may the legacy DB/schema/production
floor and DB/live-data boundary route be retired. The staged adapter is not
itself live routing or live proof. Generic approval cannot clear this blocker.

## 8. Exact future execution ordering

Phase 8 may begin only after the blocker in Section 7 is cleared by a separate
authorized implementation route.

1. Confirm the exact target and current live graph under the currently live
   pre-cutover AHL.
2. Establish the concrete newborn DB Boundary path and validate it before
   changing the legacy DB/production floor.
3. Bind the future activation Work Unit under the live policy: exact scope,
   Target, Operation, effects, exclusions, Recovery/abort basis, and
   validation.
4. Create the complete pre-cutover legacy graph savepoint/snapshot. The
   known-good source baseline is the current live graph represented by
   `4af6316b704fa5235778f92512f74dfc9f27ffa0`; the full live restore unit,
   including existing and absent destination paths, must be recorded.
5. Establish the operator-controlled admission barrier.
6. Reach and record `QUIESCENT`. If `NOT_QUIESCENT`, stop and preserve the
   live legacy graph.
7. Resolve known in-flight occurrences and conserve unknown
   allowance/reservation state. Do not carry legacy approval unless Section 6
   proves exact reconstructability.
8. Prepare the eight-file activation manifest and verify each source hash and
   destination role while the barrier remains held.
9. Replace/create all eight canonical live destinations without exposing a
   dispatchable mixed graph.
10. Validate the complete newborn live graph using Section 9.
11. If validation fails before newborn dispatch, execute the coherent legacy
   abort path in Section 10. Do not delete legacy owners first.
12. If validation passes, and only then, remove `risk-levels.md` and
   `route-format.md` after a final reference audit; retire the legacy DB floor
   only after the DB Boundary gate is proven.
13. Remove the staged newborn runtime copies after live validation establishes
   canonical live paths as the sole runtime authority. Retain migration and
   Sentinel artifacts only as non-runtime evidence.
14. Start newborn live operation with a fresh attributable Envelope and
   release the admission barrier.

## 9. Activation validation

Validation is required immediately after the router switch and before any
legacy owner deletion or newborn dispatch. The following checks are
discriminating, not name-only checks:

1. Live entry through `AGENTS.md` resolves the canonical live
   `skills/agent-human-layer/SKILL.md`.
2. Live Skill routing resolves all seven live reference owners from canonical
   live paths, not from `newborn-staging/*`.
3. No runtime reference resolves a superseded legacy owner or a fallback
   legacy path.
4. Exactly three Operations resolve: `CHANGE`, `RESTORE`, `CONTAIN`.
5. Exactly four general Evidence states resolve:
   `DECLARED`, `OBSERVED`, `VERIFIED`, `UNEVALUATED`.
6. Exactly four factual Levels resolve: AHL1, AHL2, AHL3, AHL4; no AHL5/AHL6
   numeric Level is active.
7. Authorization blockers are exactly `APPROVAL_REQUIRED`,
   `PREREQUISITE_REQUIRED`, and `BOUNDARY_REQUIRED`.
8. S055 passes: an explicitly requested Level with no attributable grant
   produces `APPROVAL_REQUIRED`, not `PROCEED`.
9. Active execution context remains a candidate until Target Binding is
   established.
10. The newborn Boundary path is live, derives the exact DB/production
    requirement, recognizes exact attributable target/effect authority, and
    its adapter/path validation passes. The staged implementation exists, but
    this independent activation check remains pending.
11. The newborn Release path proves exact artifact-to-Target Binding and
    temporal post-act validation.
12. The newborn Recovery path proves per-use applicability, no Fast credit
    from declaration alone, and local failure suspension.
13. Policy-basis identity/version semantics resolve to live `ahl-flow.md`.
14. The 56 declarative Sentinels remain present as migration evidence, with
    S055 and both S056 paths represented in the live validation selection.
15. No mixed graph exists during or after the barrier window.

Additional smoke checks should exercise wrong-target handling (S036–S039),
unknown allowance conservation (S019–S021 and S053), Route stop/violation
(S011–S012), provider-local failure (S040–S041), and Reality contradiction
(S044–S046). The repository has no executable Sentinel harness; declarative
Sentinel presence is sufficient until a separately authorized harness exists.

## 10. Abort and rollback boundary

### Before any newborn state-changing dispatch

If any activation validation fails while the admission barrier is held:

1. stop the activation and keep the barrier held;
2. do not delete legacy owners or staging sources;
3. restore the complete known-good legacy graph as one coherent replacement,
   including the six current live AHL files and the absence of newborn-only
   live destinations;
4. validate the restored live entry, router, owner references, and legacy
   blocker/recovery/release paths; and
5. release admission only after the legacy graph is coherent and validated,
   or stop with the barrier held for a new authorized recovery action.

The rollback target is the complete pre-cutover legacy graph, backed by the
pre-cutover full live-graph snapshot and the known-good source baseline. A
partial file-by-file restoration is forbidden because it would create a mixed
graph.

### After newborn dispatch has begun

Router rollback alone does not restore world state. If any newborn-governed
state-changing occurrence has dispatched, stop additional admission and expose
the actual state and Evidence. Any restoration, containment, or repair is a
new independently classified and authorized Work Unit using newborn Flow,
Target, Boundary, Recovery, Release, and Authorization semantics as
applicable. Only after the resulting state is safely handled may a separately
authorized graph rollback be considered.

## 11. Post-activation cleanup

After successful activation and live validation:

- remove superseded `risk-levels.md` and `route-format.md` once no live
  reference remains;
- retain the canonical live newborn owners only;
- remove `newborn-staging/skills/agent-human-layer/*` runtime copies so they
  cannot be mistaken for runtime authority;
- retain `newborn-staging/migration/*` and
  `newborn-staging/sentinels/*` only as non-runtime audit evidence if useful;
- retain `AHL-CANONICAL-TARGET.md` as the sole architecture SSoT; and
- perform a final search proving no dead-but-reachable legacy owner or silent
  legacy fallback remains.

There is no compatibility tail. Superseded legacy normative owners are
removed promptly after the activation and validation gates, subject to the
DB Boundary ordering above.

## 12. Future Phase 8 mutation scope

The future cutover Work Unit may touch exactly:

- the eight canonical live destinations in the activation manifest;
- the legacy `risk-levels.md` and `route-format.md` removal paths, only after
  validation;
- the staged newborn runtime copies, only after successful live validation;
- the pre-cutover full live-graph snapshot/savepoint location; and
- the bounded occurrence/allowance/reservation records required to quiesce or
  exactly migrate in-flight work.

It must not touch:

- `AHL-CANONICAL-TARGET.md`;
- `AGENTS.md` or host bootstrap;
- migration/Sentinel evidence before final retention review;
- unrelated project files, Guard, CI, database/live data, or provider state;
- any legacy file before the complete newborn graph is live and validated; or
- any live state without the applicable newborn Work Unit, Route, Boundary,
  Recovery, Release, and Authorization results.

## CUTOVER BLOCKERS

`CB-01 Human-owned policy supplied and implemented — independent validation pending`

The Human-owned DB/production Boundary policy is attributable and implemented
in staged `boundary-policy.md`: applicability is factual, the protected
requirement requires exact attributable authority for the protected DB
target/resource/effect, generic approval/access is insufficient, existing
exact authority avoids duplicate confirmation, and factual authority
provenance remains separate from Evidence. It is not yet routed by the live
newborn graph or independently validated there. Therefore the legacy
DB/production safety floor cannot yet be retired and the cutover cannot be
marked ready.

Required clearance: activate the newborn DB/production Boundary path, verify
router reachability, verify factual applicability/Target/resource/effect,
verify exact attributable target/effect authority recognition, verify Boundary
consumption and local `BOUNDARY_REQUIRED` failure, then rerun the cutover
validation. No generic approval, provider presence, or label can clear this
blocker.

## Readiness result

```text
CUTOVER_READY = false
CUTOVER_BLOCKED = true
Reason = CB-01 Human-owned policy supplied and implemented — independent validation pending
Cutover performed = false
Phase 8 begun = false
```
