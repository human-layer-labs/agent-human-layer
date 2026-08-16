# NEWBORN AUTHORIZATION POLICY — NON-LIVE STAGING

Status: `NEWBORN IMPLEMENTATION — STAGED, NOT LIVE`

This file is the sole normative owner of the newborn Closed-World
Authorization Envelope and its grant, membership, carry, allowance, and
state-transition semantics. It is not loaded by live AHL until coherent
atomic cutover.

## 1. Authorization question and ownership

Authorization answers only:

> Does this exact state-changing occurrence belong to a still-valid,
> authority-granted Closed-World Authorization Envelope?

This file owns:

- the Authorization Envelope;
- grant formation;
- Envelope forms;
- closed-world membership;
- attributable authorization provenance;
- exactly three Authorization blockers;
- carry fields and carry validity;
- active, suspended, and ended state;
- occurrence allowance and count semantics;
- reservation semantics;
- Recovery-dependent execution latitude binding; and
- informed-authorization repair.

This file does not decide:

- Goal;
- factual consequence Level;
- Target truth or Target Binding semantics;
- Recovery truth or Recovery Capability semantics;
- Boundary derivation or satisfaction;
- Release derivation or satisfaction; or
- Route selection and Route lifecycle.

It consumes the established results of those owners. `ahl-flow.md` owns
lifecycle placement, policy-basis identity/version semantics, dispatch
placement, Target Binding lifecycle, Route lifecycle, and Evidence general
semantics. This file MUST NOT redefine them.

## 2. Closed-World Authorization Envelope

Authorization is closed-world. What is not inside the attributable Envelope
is not authorized merely because it is:

- convenient;
- adjacent;
- implied by implementation;
- necessary for an Agent-preferred Route;
- technically possible; or
- reachable through repository or provider access.

The Human or attributable mandate MUST be attributable to the exact
normalized/versioned Envelope. A provenance reference and an Agent-authored
Envelope do not form a grant merely by coexisting.

Normalization MAY narrow or clarify bounds directly supported by provenance
and MAY add controls. It MUST NOT silently broaden:

- material scope;
- Target allowance;
- material effects;
- recipient or object;
- value or count;
- optional-control exceptions; or
- accepted known-unrecoverable effects.

The Envelope contains, as applicable:

- Goal or completion relation;
- allowed Operations;
- scope;
- target constraints or allowance;
- permitted material effect subset;
- exclusions;
- Boundary-related limitations or established results;
- object, recipient, value, and count limits;
- accepted known-unrecoverable effects;
- Recovery-dependent subset or execution latitude;
- requested controls;
- permitted optional exceptions; and
- Envelope end conditions.

This list describes Envelope membership inputs. It does not duplicate Target
Binding, Boundary, Release, Recovery, or Evidence semantics owned elsewhere.

An active Envelope cannot add newly discovered effects, increase its allowance,
rewrite history, expand its scope, or legalize an occurrence by editing an
Authorization policy.

## 3. Envelope forms

Exactly four Envelope forms are supported:

1. singleton;
2. finite / bounded;
3. iterative; and
4. conditional.

A singleton is an Envelope with one allowed occurrence, not a separate
authorization model.

A finite or bounded Envelope binds the permitted finite occurrence or count
range. An iterative Envelope binds the exact repeated operation/effect and
its limits. An iterative form does not create unlimited authority.

A conditional Envelope MUST bind both:

- the exact trigger; and
- the exact authorized action/effect when that trigger occurs.

This permits a pre-authorized `CONTAIN` occurrence when its exact trigger and
action are already attributable. Active harm alone creates no authority.
`CONTAIN` MUST NEVER be silently inferred into an Envelope.

## 4. Grant formation

Grant formation closes the attributable authority boundary around the exact
normalized/versioned Envelope. The Agent MUST NOT invent:

- missing material authority;
- broader scope;
- broader Target allowance;
- broader material effect;
- broader recipient, object, value, or count;
- optional exceptions;
- accepted known-unrecoverable effects; or
- additional Operations.

Goal inference MUST NOT broaden authority. Human language and shorthand are
input, not truth.

A clear isolated implementation request MAY close a same-turn Envelope when
attributable context already resolves every material authority choice. A
bounded implementation request MAY include `CHANGE` and a bounded `RESTORE`
when that relationship is already attributable and no material choice is
invented. `CONTAIN` is never silently added.

A bare task request MUST NOT manufacture unresolved material authority.

## 5. Requested caution and shorthand

Factual Level is owned by `consequence-policy.md`; this file MUST NOT recreate
a requested AHL Level as factual classification.

Wording such as `4で慎重に` MAY bind extra controls when attributable, but it
does not change factual Level. Wording such as `確認いらない`, `動くまで`,
or `1で` MAY help complete a grant only where attributable context already
closes the material Envelope. It MUST NOT silently broaden authority.

One-time shorthand is not a durable future preference. A shorthand grant
does not survive outside its attributable scope merely because an Agent
remembers it.

## 6. Membership

Before a state-changing occurrence may `PROCEED`, authorization MUST test all
applicable membership predicates:

- the Envelope is active;
- the Goal remains open and is not completed or revoked;
- the Operation is allowed;
- scope is inside the Envelope;
- the established per-effect Target Binding is a permitted member/subset of
  the Envelope allowance;
- the actual material effect subset is permitted;
- exclusions are respected;
- object, recipient, value, and count limits are respected;
- the applicable Boundary requirement is satisfied;
- required prerequisites are satisfied;
- relied Recovery applicability is satisfied;
- safety-critical ordering prerequisites hold;
- the actual next state-changing step is allowed by the current Route;
- occurrence reservation is valid where required;
- the relevant subset is not suspended;
- no Envelope end condition has occurred; and
- no Route stop condition prevents this occurrence.

Every occurrence independently matches the same grant. No authority
inheritance, self-amendment, or retroactive legalization exists.

This policy consumes established Target, Evidence, Recovery, Boundary, and
Route results. It does not redefine their owning semantics.

Route stop and Envelope end are distinct:

- a Route stop stops the current Route; and
- an Envelope end ends the Authorization Envelope.

One does not imply the other. A Route stop MUST NOT silently evaporate a
still-valid Human grant, and an Envelope end MUST NOT be represented as only a
Route stop.

## 7. Exactly three Authorization blockers

The Authorization blockers are exactly:

1. `APPROVAL_REQUIRED`;
2. `PREREQUISITE_REQUIRED`; and
3. `BOUNDARY_REQUIRED`.

No fourth Authorization blocker exists.

`ROUTE_UNDETERMINED` is a route-selection outcome owned by `ahl-flow.md`, not
an Authorization blocker. `CONFIRM_REQUIRED` is only the flow-owned
compatibility/current-turn terminal behavior and is not a fourth blocker.

### 7.1 APPROVAL_REQUIRED

Use `APPROVAL_REQUIRED` only when attributable authority is genuinely missing
for the exact occurrence or Envelope, including a missing required material
effect, count, or accepted known-unrecoverable effect.

Do not use it merely because the Agent is uncertain, reread policy, wants
reassurance, observes a factual Level change while authority is unchanged, or
is experiencing a confidence change.

### 7.2 PREREQUISITE_REQUIRED

Use `PREREQUISITE_REQUIRED` only when an actual required prerequisite is
unestablished, contradicted, or unsatisfied under the applicable owner. A
prerequisite may be a required proposition, required Evidence basis, exact
known-good target, required Recovery applicability, required validation basis,
or another concrete prerequisite.

Do not create this blocker from Agent hesitation, reread, restatement,
confidence change, internal reclassification, session change, handoff, or
semantically unchanged Route recomputation.

If reread exposes a real objective new material fact, `ahl-flow.md` decides
the earliest affected re-entry and downstream invalidation.

Machine-obtainable prerequisite facts MUST be established through the smallest
safe read-only observation before producing a Human-facing stop.

### 7.3 BOUNDARY_REQUIRED

Use `BOUNDARY_REQUIRED` only when `boundary-policy.md` determines that a
separately protected requirement exists and is not satisfied.

Authorization MUST NOT define Boundary semantics. Access, credentials,
discovery, Recovery, generic Human approval, and factual Level do not
automatically satisfy Boundary.

## 8. Authorization survival and Human Tax

A still-valid Authorization MUST survive:

- policy reread with unchanged load-bearing semantics;
- restatement;
- confidence change;
- semantically unchanged recomputation; and
- repeated bounded occurrences inside an unchanged Envelope while allowance
  remains.

Do not repeatedly ask the Human to reconfirm a valid unchanged Envelope. A
real material new fact MAY invalidate affected membership or downstream
conclusions through the flow's fixpoint.

Routine refresh MUST NOT become full reauthorization.

## 9. Policy-basis carry

Carry MUST preserve:

- original attributable Human or mandate provenance;
- exact normalized/versioned Envelope;
- active, suspended, or ended state;
- occurrence and allowance state where relevant; and
- the applicable policy basis/version/identity needed to interpret that
  Envelope.

The semantics of policy-basis identity/version are owned only by
`ahl-flow.md`. This file consumes the established identity/version and MUST
NOT redefine how it is generated or changed.

Before carry is used, mutable external Reality MUST be refreshed according to
`ahl-flow.md`.

The Human's original attributable utterance in valid context MAY serve as
provenance. An Agent summary, paraphrase, memory, or reconstruction alone
MUST NOT manufacture authority.

No universal durable authorization artifact is required for every ordinary
edit. Durable carry is required only when authorization or occurrence state
must survive a boundary that active context cannot safely preserve.

## 10. Suspension and Envelope end

Suspension and Envelope end are distinct states.

Suspension temporarily makes an otherwise authorized subset or execution
latitude unavailable while the relevant condition remains unsatisfied.

End terminates the Envelope according to its end condition or exhausted
authority.

Suspension MUST NOT silently end unrelated authorized scope. Repairing the
suspension cause MAY resume the same attributable authority when the same
material basis remains valid. Human reapproval is not required solely because
a dependent mechanism was repaired.

## 11. Recovery-dependent execution latitude

This policy owns which exact effect subset, optional exception, or execution
latitude depends on an established Recovery Capability. It consumes the
Capability and applicability result from `recovery-policy.md`.

If that Capability fails or becomes inapplicable, suspend only the dependent
subset or latitude. Do not suspend unrelated authority.

Recovery does not grant authority. Failed Recovery cannot self-authorize
repair. Repair is a separate Work Unit requiring its own valid authorization.

## 12. Informed-authorization repair

If all of the following hold:

- the authorized effect box is unchanged;
- attributable authority exists; and
- the Human was materially misinformed about aggregate consequence;

apply the narrow one-time repair:

1. suspend the affected authorization;
2. preserve actual state and effect boundaries;
3. correct the material representation; and
4. obtain reauthorization once.

The reason is materially misinformed authorization, not merely a numeric
Level mismatch. Do not repeatedly reconfirm after the corrected grant remains
valid.

## 13. Occurrences, allowance, count, and retry

Approval count is not occurrence count.

Define occurrence and allowance semantics without creating a universal
ledger. For accumulating external or material effects:

- track occurrence identity where needed;
- reserve and consume allowance;
- treat timeout or unknown result as consumed until read-only Evidence
  establishes no effect; and
- retry the same logical occurrence only when real idempotency guarantees
  that its semantics.

An Agent's inability to observe the result does not make retry free.

Durable occurrence accounting is required only where actual accumulating
effect, concurrency, retry, or carry needs it.

## 14. Reservation and concurrency

For material or critical accumulating effects where concurrency or retry can
exceed authorized limits, trustworthy occurrence reservation is part of
Authorization membership.

Reservation MUST be successfully obtained before Core dispatch. `PROCEED`
and dispatch MUST be linearized with successful reservation where the
material effect requires it.

Core dispatch placement is owned by `ahl-flow.md`; this policy owns the
reservation requirement and membership semantics.

If trustworthy reservation is unavailable, serialize execution or use
singleton authorization. Do not invent a universal durable ledger.

## 15. No authority inheritance

Work Unit relationships do not inherit authority. A child, repair, failure,
`RESTORE`, or `CONTAIN` Work Unit does not receive authorization merely from
another Work Unit.

Each occurrence and each failure Work Unit requires its own valid membership
under its applicable Envelope. Flat Work Unit authority remains compatible
with `ahl-flow.md`.

## 16. Cross-owner boundary

This file MUST NOT normatively redefine:

- lifecycle, Work Unit semantics, Operations, Evidence general semantics,
  Goal, Challenge, Arbiter, Core, Route, Target Binding, startup, policy-basis
  identity semantics, occurrence dispatch placement, or Reality collision
  from `ahl-flow.md`;
- Recovery Capability fields, Fast qualification, composition, Recovery
  Evidence sufficiency, or Recovery failure mechanics from
  `recovery-policy.md`;
- Boundary derivation or satisfaction from `boundary-policy.md`;
- Release derivation, artifact-to-Target transition rules, or Release checks
  from `release-gate-policy.md`;
- Work Unit serialization from `work-unit-format.md`; or
- activation/router behavior from `SKILL.md`.

Reference the owning policy rather than duplicating its normative rule.

## 17. Cross-file consistency

The pair of Phase 2 policies MUST preserve these distinctions:

- factual consequence is not Authorization;
- AHL4 does not automatically mean unauthorized;
- AHL1 does not automatically mean authorized;
- Human permission does not lower factual Level;
- Recovery does not lower factual Level;
- Recovery availability does not grant permission;
- Authorization does not decide Reality; and
- authorization does not replace the flow's Target, Route, Evidence,
  Boundary, Release, or Goal owners.

The flow remains compatible with this sequence:

```text
final factual classification
→ independent Boundary / Release requirements
→ Recovery / Evidence prerequisites
→ Envelope build or match
→ aggregate consequence representation
→ informed-authorization repair if materially wrong
→ Authorization membership
→ occurrence refresh
→ Act
```

This file does not activate the newborn graph, modify the frozen blueprint,
alter live routing, or authorize Phase 3.
