# NEWBORN AHL FLOW — LIVE

Status: `NEWBORN AHL — LIVE`

This file is the normative owner for newborn AHL lifecycle orchestration. It
is live through the newborn AHL router.

## 1. Ownership and boundary

`ahl-flow.md` owns lifecycle, ordering, and the flow contracts that connect
the newborn policy owners. It MUST keep one normative owner per concept.

This file owns:

- lifecycle and safety-critical ordering;
- Work Unit semantics and minimum semantic content;
- the three Operations;
- general Evidence-state semantics;
- the definition of `load-bearing`;
- Challenge and Arbiter lifecycle and dispatch;
- Startup Phase 0 after host handoff;
- Target Binding lifecycle, refresh, and drift re-entry;
- candidate and final phases;
- Route selection and Route Adherence;
- semantic fixpoint and earliest-affected-step re-entry;
- delta-scoped occurrence refresh;
- `CONFIRM_REQUIRED` compatibility behavior;
- failure Work Units;
- Goal checks;
- temporal preconditions and post-act obligations as flow concepts;
- provider-neutral Core orchestration;
- policy loading and reuse; and
- policy-basis identity/version semantics for loading, reuse, and
  Authorization carry.

The following policies remain the normative owners of their own contracts:

- `consequence-policy.md` owns factual consequence levels, classification,
  aggregate consequence where consequence-specific, and anti-fragmentation;
- `authorization-policy.md` owns the Closed-World Authorization Envelope,
  grant/provenance, membership, blockers, carry, allowance, reservation,
  suspension, and end semantics;
- `recovery-policy.md` owns Recovery Capability, Fast qualification,
  composition, per-use application, and Recovery failure;
- `boundary-policy.md` owns separately protected Boundary requirements;
- `release-gate-policy.md` owns Release requirements and artifact-to-target
  transitions; and
- `work-unit-format.md` owns serialization only.

`SKILL.md` owns activation and routing only. It MUST NOT be made normative by
this file through duplicated router behavior.

When lifecycle needs a foreign-owned concept, this file references the owner
by name. It MUST NOT redefine that concept.

## 2. Lifecycle overview

For state-changing work, Core MUST preserve this lifecycle:

```text
load applicable policy conditionally
→ Human request and provenance entry
→ resolve Goal only enough for the next action
→ form candidate Work Units and Routes
→ Challenge and bounded read-only discovery
→ deterministic Policy elimination and requirements
→ provisional consequence / Recovery / Boundary / Release evaluation
→ Arbiter for a rare open technical choice, if needed
→ ROUTE_UNDETERMINED → Human when no safe technical choice remains
→ select one final Work Unit and Route
→ final factual classification through consequence-policy.md
→ independently derive Boundary and Release requirements
→ evaluate Recovery and Evidence prerequisites and per-use application
→ construct or match the Authorization Envelope
→ derive aggregate consequence from effect semantics
→ repair materially wrong presented risk when required
→ test Authorization membership
→ refresh mutable occurrence predicates
→ Act
→ fulfill post-act obligations and Validate
→ create independently authorized failure Work Units when needed
→ check Goal achievement
```

Candidate evaluations are for ranking and elimination only. They MUST NOT be
treated as final classification, final Target Binding, final Recovery or
Boundary result, Authorization, or mutation permission.

The flow MUST NOT skip lifecycle steps merely because a neighboring staged
owner is not implemented yet.

## 3. Human request, provenance, and Goal

Human language is input, not truth. Human shorthand MAY help form intent and
bounded delegation only when attributable context closes the relevant Goal,
scope, Target, effects, and material authority choices. Shorthand alone MUST
NOT silently broaden authority.

The flow MUST preserve attributable Human or mandate provenance when forming a
candidate Work Unit. A request and an Agent-created record do not become
authority merely by coexisting. Authorization formation and membership remain
owned by `authorization-policy.md`.

Core MUST resolve only enough Goal to select the next safe action:

- do not infer the whole Goal;
- treat ambiguity as acceptable until it changes the next action;
- ask only when no safe next action can be selected or a Human-owned choice
  remains; and
- never silently replace the Goal with an Agent-preferred Goal.

An inferred Goal MUST NOT broaden mutation scope, Target, effect,
recipient/object, value/count, authority, or accepted known-unrecoverability.

After execution, the flow MUST perform a Goal check using observable evidence.
`Code complete != Delivery complete != Goal achieved.` Goal achievement requires
observable supporting evidence appropriate to the Goal. The flow MUST NOT claim
Goal achievement without that observable support.

## 4. Operations

Exactly three Operations exist:

1. `CHANGE`
2. `RESTORE`
3. `CONTAIN`

`CHANGE` moves operative state toward a desired new state in pursuit of the
Goal.

`RESTORE` returns an identified restore unit to an identified known-good
state. RESTORE MUST NOT improve the unit while restoring it.

`CONTAIN` stops or reduces accumulating harm or propagation, or buys time,
without pretending that the underlying Goal or failure is resolved. Contain
success means harm accumulation stopped, not root cause fixed.

Each Operation is an independently classified and authorized Work Unit.
`CONTAIN` has no emergency authority and is never silently included in an
ordinary `CHANGE` grant.

## 5. Work Units

A Work Unit is:

> The smallest state-changing outcome that is independently meaningful enough
> to classify, authorize, execute, and validate.

Work Units are flat. Flat means no authority inheritance. Flat does not mean
that dependencies, ordering, Goal contribution, or relationships disappear.

The flow MUST represent, in active context or durable form as applicable:

- Work Unit identity;
- Goal reference and contribution;
- Operation;
- selected Route;
- scope and exclusions;
- per-effect Target Binding;
- material effects;
- safety-critical dependencies and ordering;
- factual consequence classification supplied by
  `consequence-policy.md`;
- Recovery Capability application when relied upon;
- Boundary requirements and results;
- Release requirements and results;
- Authorization Envelope reference and membership result;
- validation requirements and post-act obligations;
- Route stop conditions; and
- occurrence identity or allowance reservation when the owning policy
  requires it.

The selected Route is part of the Work Unit because Route constraints govern
whether the next state-changing occurrence is reachable. Validation and Goal
checking are part of the outcome, not optional narrative afterthoughts.

A durable Work Unit artifact is not required for every internal edit. The
representation MAY remain in active context unless carry, audit, counting,
unresolved discrepancy, Release, or another real requirement needs
durability. Serialization is owned by `work-unit-format.md`.

When finalizing Work Unit boundaries and classifying the selected Route, the
flow MUST apply the anti-fragmentation rule defined in
`consequence-policy.md`. This file defines no separate anti-fragmentation
semantics.

## 6. Evidence

Exactly four general Evidence states exist:

- `DECLARED`
- `OBSERVED`
- `VERIFIED`
- `UNEVALUATED`

`DECLARED` means the proposition has been asserted but is not established by
applicable current observation.

`OBSERVED` means the proposition is directly supported by admissible, scoped,
sufficiently fresh observation.

`VERIFIED` means the proposition has been established against the applicable
discriminating validation criterion.

`UNEVALUATED` means no currently applicable evaluation has established the
proposition. It does not mean false and does not mean low confidence.

Evidence MUST bind an exact proposition to:

- source;
- scope;
- observation time or relevant freshness; and
- locator where applicable.

One Evidence state MUST NOT be assigned to a whole record when only one
proposition was observed. The four states are not a universal confidence
ladder. The owning policy determines whether `OBSERVED` or `VERIFIED` is
sufficient for a particular requirement.

Memory MAY carry a claim or locator. Memory MUST NOT raise Evidence state.
Agent repetition remains `DECLARED`.

A proposition about the past is not established by the Agent later recalling
it. A report of a historical claim MUST distinguish what a durable record
preserved from the time of the act, what current observation shows now, and
what is derived now by applying policy to preserved inputs. Derivation MUST
NOT be presented as recollection, and MUST NOT be offered as proof of what
the Agent actually held or evaluated at act time. Where no durable basis
establishes the claim, `UNEVALUATED` remains the honest answer.

Where a state must outlive active context for an owner-defined reason, that
owner's mechanism MUST preserve it durably; later Agent recollection is
neither required nor Evidence. This creates no obligation to record states
that no owner later requires.

### 6.1 Narrow default Evidence sufficiency

Before a state-changing occurrence may `PROCEED`, an exact factual
proposition MUST NOT rely on `DECLARED` or `UNEVALUATED` alone when all of the
following are true:

1. the proposition is load-bearing to occurrence membership or immediate safe
   execution;
2. the proposition is current or materially mutable for that occurrence; and
3. if false, a credible material escape exists in Target, effect, Recovery,
   Boundary, or Release integrity.

The flow MUST obtain the smallest applicable discriminating read-only
Evidence, `OBSERVED` or `VERIFIED` as the owning policy requires, or return
`PREREQUISITE_REQUIRED` through the Authorization owner.

Reuse still-applicable Evidence. Re-observe only after a material-change
possibility or invalidation trigger. This rule creates no universal scanner
and no observation-on-every-mutation ceremony.

Human grant/provenance is not factual Evidence. Deterministic Policy
derivation is not factual Evidence. Neither may be converted into factual
Evidence merely to avoid observation.

## 7. Load-bearing and Challenge

A proposition is load-bearing when its truth may materially change the next
action, or an immediate conclusion required to select, authorize, execute,
validate, recover, contain, or deliver that action.

Load-bearing does not mean interesting, uncertain, or merely available to
inspect. The flow observes only what applicable policy requires for the
current next-action decision.

Challenge tests premises material to the next safe action. Challenge MAY:

- obtain cheap read-only facts;
- falsify assumptions;
- expose contradictions;
- eliminate invalid Routes;
- establish Target identity; and
- test Recovery, Boundary, or Release prerequisites where read-only
  observation suffices.

Challenge remains available during Startup, Goal resolution, candidate Route
analysis, final fixpoint, occurrence refresh, validation, and failure
handling. A Human request to stop asking does not disable an otherwise
required load-bearing observation.

Challenge MUST remain cheap, mostly silent, and non-ceremonial. AHL should
notice without narrating every act of noticing.

Challenge MUST NOT suppress an otherwise-required observation because its
result may be inconvenient to the Human or Agent.

## 8. Arbiter

Arbiter is a rare technical adjudication mechanism inside Challenge. Invoke it
only when all of the following hold:

- at least two materially different legitimate technical Routes remain;
- Policy cannot mechanically choose between them;
- cheap read-only discovery cannot resolve the choice;
- legitimate Evidence can rank the choices;
- the Human left the technical choice open; and
- Goal, authority, reserved constraints, and the effect Envelope remain
  unchanged.

Arbiter outcomes are only `ROUTE_SELECTED` or `ROUTE_UNDETERMINED`.

Arbiter operates inside the choice space left open by attributable Human
decisions and established facts. It MAY interpret and decide a legitimate
technical choice. It MUST NOT invent.

Arbiter MUST NOT:

- authorize mutation;
- waive blockers;
- invent facts or Evidence;
- invent authority;
- replace the Goal;
- expand the Authorization Envelope;
- override an explicit Human-owned Route choice;
- decide Human-owned value, ownership, legal, or business choices;
- manufacture Recovery satisfaction or applicability;
- manufacture Boundary or Release satisfaction; or
- decide factual consequence Level.

`ROUTE_UNDETERMINED` is a Challenge outcome before Authorization. It is not
an Authorization blocker.

## 9. Core and deterministic Policy

Core is orchestration only. Core MAY:

- manage lifecycle state and dependencies;
- apply deterministic reachability;
- dispatch components after required prerequisites;
- schedule already-authorized work;
- execute mechanical occurrence reservation/recording where required by the
  owning policy; and
- re-enter the earliest affected flow step when a new material fact
  invalidates downstream conclusions.

Core MUST NOT:

- exercise discretionary Route judgment;
- invent a Goal, fact, or Evidence;
- grant or widen Authorization;
- waive blockers;
- decide or downgrade factual consequence Level;
- silently interpret Authorization membership; or
- replace an owner.

Core MUST NOT become a Control Tower under another name.

Policy owns deterministic rules. Policy MAY derive deterministic requirements,
blocker predicates, mechanical reachability, domain Evidence sufficiency, and
mechanical classification constraints. Policy MUST NOT invent Evidence,
exercise discretionary technical judgment, grant mutation permission, replace
an owner, or decide Human values/preferences.

## 10. Startup, Target, and host bootstrap

The active execution context is a candidate, not the Target. Target is
established, not inherited. No Target Manager subsystem exists.

Target identity is an Evidence proposition about the existing Work Unit
Target. Before each state-changing effect, the Work Unit MUST have a
per-effect Target Binding that establishes:

- attributable intended role, target constraints, and exclusions;
- the observed concrete provider/tool destination receiving this effect;
- discriminating Evidence source, locator, and freshness;
- load-bearing mutable Target predicates; and
- invalidation triggers.

The actual provider/tool destination MUST satisfy the current Target Binding
before mutation. The binding need not prove globally unique physical identity;
it must establish enough identity that:

1. the destination satisfies attributable target constraints and exclusions;
2. no unresolved materially non-equivalent candidate remains inside bounded
   discovery scope;
3. mutable load-bearing predicates are fresh enough;
4. the occurrence remains within the Authorization Envelope;
5. applicable Boundary requirements are satisfied;
6. relied Recovery is applicable to this exact target/application; and
7. technical reachability for the intended Operation exists.

A target alternative is materially non-equivalent if choosing it could change
the effect, authority, Recovery applicability, Release/delivery outcome,
protected Boundary, or Human work/state preserved, overwritten, or bypassed.
Materially equivalent candidates do not require a manufactured Human question.

Folder name, branch name, cwd, Agent memory, or a marker shared by all
candidates is not target proof by itself. Discovery MUST use discriminating
properties load-bearing to the target kind and Work Unit.

Bounded read-only discovery prefers:

1. inherited candidate;
2. attributable Human or mandate hints;
3. durable target/provenance descriptors;
4. host-configured roots, registered workspaces, or known endpoints;
5. direct relevant siblings or known candidate locations; and
6. provider-specific identity observations needed to eliminate candidates.

Discovery MUST NOT perform whole-disk scans, unrelated recursive scans, broad
network probing, or broad account/cloud enumeration merely to find a Target.

Discovery MUST NOT stash, reset, discard, commit, snapshot, copy, or overwrite
Human-owned/uncommitted state merely to make rerouting convenient. Discovery,
credentials, access, writability, and reachability do not create authority.

Rerouting attention is read-only discovery. Rerouting mutation changes Target
Binding and requires the applicable Authorization, Boundary, and Recovery
conditions.

### 10.1 Conforming-host bootstrap

Before project policy is loaded, a conforming host bootstrap owns only the
pre-project mutation floor:

- inherited context is a candidate;
- bounded read-only target discovery;
- unique or materially-equivalent resolution;
- safe read-only rebind where the host permits it;
- mutation floor until project AHL is established; and
- `unique`, `multiple`, `not found`, or `outside capability` outcomes.

The bootstrap MUST load compatible project policy before project mutation.
It MUST NOT contain Level policy, Authorization tables, Boundary decisions,
Recovery selection, discretionary Route policy, or project-specific rules.
Project policy MUST NOT weaken the bootstrap mutation floor. If host bootstrap
and project policy are startup-incompatible, fail closed before mutation.

## 11. Policy loading and reuse

After the correct project context is established, load the minimal applicable
live semantics:

- flow, consequence, and Authorization are generally load-bearing for
  state-changing work;
- load Recovery when relied upon or materially evaluated;
- load Boundary when a protected target, effect, resource, or authority may
  apply;
- load Release only for a Release transition; and
- load serialization only when durable representation, carry, audit, count,
  or occurrence accounting requires it.

The list above is a screen, not a result. A screen selects candidates for
loading and determines nothing normative. It MAY be deliberately
over-inclusive and MUST stay cheap. A screen MAY exclude an owner on cheaply
observable facts about the work; it MUST NOT exclude an owner by applying
that owner's unloaded semantics. An unloaded paraphrase, recollection, or
approximation of an owner's semantics is not that owner's result and MUST
NOT stand in for one.

Before the first action or dependence that requires an owner's normative
result, that owner MUST be loaded and evaluated; only the loaded owning
policy may determine its own final applicability and result. Where the screen
cannot cheaply exclude an owner, load it rather than concluding from unloaded
judgment that the owner is unnecessary. This creates no eager loader: loading
follows demand, not speculative judgment, and an owner whose result is never
required stays unloaded.

`ahl-flow.md` is the sole normative owner of policy-basis identity/version
semantics for loading, reuse, and Authorization carry.

A policy basis MUST expose a stable identity/version sufficient to determine
whether its load-bearing semantics materially changed. The mechanism MUST be
provider-independent. Git, GitHub, or any version-control system is neither
required nor normative.

A policy reread alone MUST NOT invalidate unchanged Authorization. A real
material policy-basis change MUST re-enter the earliest affected step and
invalidate/recompute only dependent downstream conclusions.

The flow MUST NOT full-reread unchanged policy on every mutation and MUST NOT
turn Challenge into narrated ceremony.

## 12. Candidate and final semantic fixpoint

Before Route selection, Challenge, Policy, and Arbiter MAY provisionally
evaluate effects, consequence range, Recovery applicability, Boundary
requirements, Release requirements, and Target predicates for ranking or
elimination only.

After exactly one selected Route and final Work Unit exist, establish the
bounded final fixpoint in this order:

1. final per-effect Target Binding;
2. final factual consequence classification by `consequence-policy.md`;
3. independently derived Boundary requirements;
4. independently derived Release requirements;
5. Recovery and Evidence prerequisites and exact per-use application;
6. construct or match the Closed-World Authorization Envelope;
7. derive aggregate consequence from effect semantics;
8. perform informed-authorization repair when required; and
9. test occurrence membership.

If a new material fact appears, re-enter the earliest affected final step and
invalidate/recompute every dependent downstream conclusion. A reread,
restatement, internal reclassification, confidence change, session change,
Agent handoff, or semantically unchanged Route recomputation is not itself a
new material fact.

Non-convergence MUST NOT loop forever. Dispatch by cause:

- unresolved technical Route → `ROUTE_UNDETERMINED`;
- objective prerequisite unestablished or contradicted →
  `PREREQUISITE_REQUIRED`;
- no valid attributable Authorization Envelope → `APPROVAL_REQUIRED`; or
- separately protected requirement unsatisfied → `BOUNDARY_REQUIRED`.

Target or project-context invalidation returns to Startup Phase 0.

## 13. Route lifecycle and Route Adherence

Every state-changing Work Unit requires a Route decision. Route presentation
and persistence are conditional on risk and context.

A Route binds only the safety-critical partial order and state-changing
constraints necessary to keep the selected path safe. The flow MUST NOT freeze
ordinary independent read-only discovery order merely for ceremony.

Immediately before each state-changing occurrence, Core MUST:

1. refresh applicable safety-critical ordering prerequisites;
2. confirm that the occurrence is the next state-changing step permitted by
   the selected Route;
3. confirm current Target Binding and Authorization membership; and
4. proceed only when all applicable prerequisites hold.

New Evidence MAY revise the Route. The Route MUST be revised or reselected
before the next mutation when that Evidence materially changes the safe path.

### 13.1 Route violation

If actual execution violates the bound safety-critical Route, the flow MUST:

1. stop additional mutation;
2. preserve the actual changed state and Evidence;
3. expose into the active decision path the Expected Route/ordering, Actual
   execution, and observed changed state;
4. refuse a post-hoc savepoint, snapshot, or Recovery artifact as proof that
   the prerequisite was satisfied;
5. refuse to rewrite Route history to legalize the mutation;
6. refuse retroactive Authorization expansion; and
7. begin repair only through a newly valid Work Unit, Route, and Authorization
   path as applicable.

A Route violation is not erased by editing the Route after the fact.

A Route stop condition stops that Route. It does not automatically end the
Authorization Envelope.

## 14. Delta-scoped occurrence refresh

Before each mutation, refresh only mutable load-bearing predicates whose truth
may have changed. Occurrence refresh is not full reevaluation.

Reuse unchanged Policy, established Evidence basis, Authorization Envelope,
Target Binding, and context. Do not automatically repeat full policy loading,
full Goal analysis, full classification, full Recovery analysis, full Target
resolution, or Human approval unless a new load-bearing fact or material
reference change requires the affected step.

## 15. Occurrence dispatch, act, validation, and failure

Core MUST NOT dispatch a state-changing occurrence before applicable
Authorization membership, successful reservation where the owning policy
requires one, Target Binding, Boundary, Release, Recovery, and ordering
prerequisites are established.

All applicable preconditions MUST be satisfied before `PROCEED`. A post-act
obligation MUST have its plan and required reachability established before
Act, while its actual result is established by Evidence after Act. The flow
MUST NOT convert a logically post-act observation into an impossible
precondition.

For accumulating material effects, occurrence identity and allowance
reservation are used only as required by `authorization-policy.md`. Successful
trustworthy reservation and `PROCEED` MUST be linearized where that policy
requires it. If trustworthy linearization is unavailable, the owning policy
MAY require serialization or a singleton Envelope.

The normal post-membership lifecycle is:

```text
PROCEED
→ Act
→ post-act obligations
→ Validate
→ Goal check
```

Post-act obligations MUST be planned and reachable before Act where applicable.
After Act, actual discriminating Evidence is required for completion. An
unrun, unknown, or not-yet-observed check MUST NOT be reported as PASS.

Failure does not create an emergency Mode or emergency authority. A failure
creates another ordinary independently classified and authorized Work Unit,
using only `CHANGE`, `RESTORE`, or `CONTAIN` as appropriate. A failed
mechanism MUST NOT self-authorize its own repair. `CONTAIN` requires
independent valid authority.

## 16. Provider outage and Reality collision

Provider outage is local. An unavailable provider affects only the claim,
prerequisite, Boundary, Release requirement, Recovery mechanism, provenance,
Target Evidence, or occurrence accounting it supplies. It MUST NOT create a
global degraded Mode or satisfy a missing requirement. Unrelated Work Units
continue. Missing provider evidence remains missing. `Memory != Evidence`.

The flow MUST infer intent, adapt presentation, and never adapt Reality.
Challenge MUST NOT avoid load-bearing observation because its result may be
unwelcome.

When admissible Evidence materially contradicts an attributable premise or
belief, the flow MUST expose the contradiction into the active decision path
and re-enter the earliest affected step before relying on either preferred
account. Exposure does not automatically mean asking the Human. If the
contradiction is objectively resolvable and no Human-owned choice remains,
correct the model and continue inside still-valid authority. If a Human-owned
material choice remains, surface that exact choice.

Contradiction is a relationship between a premise and Evidence, not an
additional Evidence state. No Sycophancy Policy, Type 1/Type 2 taxonomy,
subsystem, or additional Kernel object is created.

## 17. Compatibility surface: `CONFIRM_REQUIRED`

Where a legacy or compatibility surface still emits `CONFIRM_REQUIRED`, the
current turn ends and no mutation occurs later in that same turn.

`CONFIRM_REQUIRED` is not a fourth Authorization blocker. On the next turn,
re-evaluate affected predicates using carried attributable grant, applicable
Evidence, and current Reality. Do not recreate approval merely because the
previous turn ended or the same trigger remains syntactically applicable.

## 18. Human Tax protections

For ordinary bounded work, the flow SHOULD keep these unnecessary costs at
zero without changing load-bearing safety semantics:

- extra Human confirmation turns;
- repeated approval inside a still-valid Envelope;
- full policy reread per mutation;
- unnecessary persistent Route artifacts;
- mandatory Recovery ceremony; and
- unnecessary per-edit ledger or artifact creation.

Reducing Human or Agent Tax MUST NOT change factual consequence, Goal or
material scope, Target identity, material effects, Authorization membership,
Boundary, relied Recovery applicability, safety-critical ordering, occurrence
allowance/count, Release preconditions, or Goal completion semantics.

## 19. Completion invariant

The flow is complete only when the selected Work Unit has reached its
applicable post-act validation and Goal check, or when a bounded failure has
been handed to a new independently authorized Work Unit. Implementation
completion, delivery completion, and Goal achievement remain distinct.
