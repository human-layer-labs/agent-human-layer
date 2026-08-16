# AHL Canonical Target — Newborn Architecture Candidate

Status: **NEWBORN BLUEPRINT FROZEN**  
Purpose: **Single architecture target for newborn canonical implementation and atomic migration. Not live execution policy.**  
Audit state: **Final narrow freeze audit completed; findings NONE.**  
Legacy Core baseline: `4af6316b704fa5235778f92512f74dfc9f27ffa0`  
Legacy Guard baseline: `af30ee69fd2782c075d1d70438c6c3b43ad0ea51`

Canonical architecture metadata: `AHL-CANONICAL-TARGET.md` is the sole canonical architecture SSoT. Copies, notes, Obsidian files, audit excerpts, generated summaries, and Agent memory are non-canonical.

This document is the **single architecture target** for writing the newborn AHL.

It is not a second runtime policy layer.  
During implementation, each operational concept has exactly one normative runtime owner in the canonical file set defined below.  
After atomic newborn cutover, live Agents load those runtime owners, not this architecture target as a parallel policy source.  
This document remains a frozen architecture/migration/audit reference unless a later architecture revision explicitly supersedes it.

Do not redesign this architecture during canonical writing.  
Do not introduce a competing authority mechanism.  
Do not reopen fixed Human decisions.  
Do not preserve conflicting legacy semantics merely for compatibility.  
Do not modernize legacy AHL merely to ease migration.  
If current canonical text conflicts with this target, report the conflict and implement the target through the designated normative owner.

---

## 1. Architecture identity

### Bounded Freedom

**Bounded Freedom is what AHL gives the Human.**

The Human speaks naturally in goals, constraints, preferences, shorthand, and delegation.  
The Human should not need to understand internal AHL schemas.

### Closed-Envelope Kernel

**Closed-Envelope Kernel is how AHL provides Bounded Freedom.**

AHL keeps these semantics separate rather than collapsing them into one safety score or Mode:

- Goal
    
- Work Unit
    
- Route
    
- Operation
    
- Challenge / Arbiter
    
- factual consequence / AHL Level
    
- Evidence
    
- Target Binding
    
- Recovery Capability
    
- Boundary
    
- Release
    
- Authorization Envelope
    
- occurrence identity / allowance when required
    
- deterministic Policy
    
- Core orchestration
    

This list describes the core semantic surface. It is not a license to create one subsystem per noun.  
Several are flow-owned semantics, not independent managers.

Core principles:

> **Human grants breadth. Recovery grants speed.**

> **AHL should absorb complexity, not export it.**

> **Dangerous boundaries are extremely hard. Everything else is almost transparent.**

The front should feel simple.  
The back should be precise.

The ultimate direction remains:

> **The ultimate goal of AHL is to make the layer disappear.**

---

## 2. Belief trunk and literal implementation delta

The following are **architecture/trunk principles carried into the newborn target**. Their presence here does **not** mean they are all literal additions to `BELIEF.md`:

> Ask.  
> Challenge.  
> Act.  
> Restore.

`CONTAIN` is a special form of Act.  
Arbiter is a mechanism inside Challenge.  
There is no fifth trunk verb.

> Follow the Goal, not the request.  
> Change the Route, not the Goal.  
> Challenge the Goal, but never replace it silently.

> Ambiguity is acceptable until it changes the next action.  
> When no safe next action can be chosen, ask.

> A rollback path must be cheap enough to actually use.

> Correctness is a tactic.  
> Trust is the infrastructure.  
> The goal is the goal.

### Literal `BELIEF.md` implementation delta

Add exactly one new Belief sentence:

> **Human authority grants freedom to act; demonstrated recovery makes that freedom cheap to use.**

Apply exactly these three narrow rewords, including the existing headings/claims they replace:

- `The chat is the control tower.`  
    → `The chat is the Human interface.`
    
- `Snapshot is recovery.`  
    → `Recovery returns a known-good state. A snapshot is one possible mechanism.`
    
- `GitHub is audit.`  
    → `Audit records what happened. GitHub is one possible audit provider.`
    

Do **not** add `Correctness is a tactic...` or `A rollback path must be cheap enough to actually use.` to `BELIEF.md` merely because this architecture target quotes them.  
No new Belief chapter or decorative Belief growth is required.

### Narrow `CHEAP-DEATH.md` authority rewrite before cutover

Replace exactly:

> `The human is absolute over decisions.`

with:

> **The Human is final over decisions within authority attributable to that Human.**

Architecture authority invariant:

> An instruction carries authority only within authority attributable to its source.

Runtime authority semantics remain owned by `authorization-policy.md`.  
Reality-collision / sycophancy handling requires no additional Belief sentence.

---

## 3. Primary safety and Tax rule

AHL must not purchase safety by exhausting Human attention or by creating hidden Agent bureaucracy.

For ordinary bounded work, the target is:

- extra Human confirmation turns = 0
    
- repeated approval inside a still-valid Envelope = 0
    
- full policy reread per mutation = 0
    
- unnecessary persistent Route artifact = 0
    
- mandatory Recovery ceremony = 0
    
- unnecessary per-edit ledger/artifact = 0
    

Human Tax and unnecessary Agent Tax are both design failures.

A safety mechanism that is too expensive to use will eventually be bypassed.

Tax reduction is invalid if it changes any load-bearing safety semantic, including:

- factual consequence
    
- Goal or material scope
    
- Target identity
    
- actual material effects
    
- Authorization membership
    
- Boundary requirement
    
- relied Recovery applicability
    
- safety-critical ordering
    
- occurrence allowance/count
    
- Release preconditions
    
- Goal completion semantics
    

---

## 4. Human intent, adaptation, and Reality collision

Human language is input, not truth.

Taking Human words only literally is insufficient.  
The Agent must infer enough Human intent to choose the next action.

Presentation may adapt.  
Tone may adapt.  
Terminology may adapt.  
Explanation may adapt.

**Reality may not adapt.**

Canonical invariant:

> **Infer intent. Adapt presentation. Never adapt facts.**

Neither Human preference nor Agent preference may substitute for established Reality.

Challenge must not suppress or avoid an otherwise-required load-bearing observation merely because its result may conflict with Human or Agent expectation.

When admissible observed Evidence materially contradicts an attributable premise or belief:

> **Expose the contradiction into the active decision path and re-enter the earliest affected step before relying on either preferred account.**

“Expose” does not automatically mean “ask the Human.”

If the contradiction is objectively resolvable and no Human-owned decision remains, the Agent corrects its model and continues inside the still-valid Envelope.  
If a Human-owned material choice remains, surface that exact choice.

The contradiction is a relationship between a premise and Evidence.  
It is not a fifth Evidence state.

No `Sycophancy Policy`, subsystem, taxonomy, or additional Kernel object exists.  
“Type 1 / Type 2 忖度” remains audit vocabulary only.

---

## 5. Platform independence

AHL Kernel must not depend on:

- Git
    
- GitHub
    
- GitLab
    
- Guard
    
- CI
    
- GitHub Actions
    
- pull requests
    
- issues
    
- branches
    
- filesystem snapshots
    
- any specific source-control platform
    
- any specific cloud, storage, database, or deployment provider
    

These may be providers/adapters for:

- Evidence
    
- Recovery
    
- audit
    
- provenance
    
- Release control
    
- Boundary evidence
    
- target identity
    
- coordination
    
- occurrence accounting
    
- shared state
    

None defines the Kernel.

Provider outage is local:

> An unavailable provider affects only the claim, prerequisite, Boundary, Release requirement, Recovery mechanism, provenance, target Evidence, or occurrence accounting that it supplies. It neither creates a global degraded Mode nor satisfies the missing requirement. Unrelated Work Units continue.

No special offline/degraded Mode is required.

`Memory ≠ Evidence.`

---

## 6. Canonical runtime file architecture

```
BELIEF.md

skills/agent-human-layer/
├─ SKILL.md
└─ references/
   ├─ ahl-flow.md
   ├─ consequence-policy.md
   ├─ authorization-policy.md
   ├─ recovery-policy.md
   ├─ boundary-policy.md
   ├─ release-gate-policy.md
   └─ work-unit-format.md
```

One concept has one normative runtime owner.  
Other files may reference it; they do not restate it normatively.

### `ahl-flow.md`

Owns:

- lifecycle and ordering
    
- Work Unit semantics and minimum semantic content
    
- exactly three Operations
    
- general Evidence-state semantics
    
- definition of `load-bearing`
    
- Challenge / Arbiter lifecycle and dispatch
    
- Startup Phase 0 after host handoff
    
- Target Binding lifecycle / refresh / drift re-entry
    
- candidate vs final phases
    
- Route selection and Route Adherence lifecycle
    
- bounded semantic fixpoint
    
- earliest-affected-step re-entry
    
- delta-scoped occurrence refresh vs full reevaluation
    
- `CONFIRM_REQUIRED` current-turn compatibility semantics
    
- failure Work Units
    
- Goal check
    
- temporal preconditions vs post-act obligations as flow concepts
    
- provider-neutral Core orchestration contract
    
- policy loading and reuse
    
- policy-basis identity/version semantics for loading, reuse, and Authorization carry
    

### `consequence-policy.md`

Owns:

- AHL1–AHL4 definitions
    
- classifier
    
- AHL2/AHL3 distinction
    
- aggregate factual consequence semantics where consequence-specific
    
- anti-fragmentation
    
- exclusions from Level
    
- classification actor contract
    

It must not own permission, Recovery semantics, Boundary ownership, Release authority, or Human shorthand profiles.

### `authorization-policy.md`

Owns:

- Closed-World Authorization Envelope
    
- exact grant/provenance binding
    
- Envelope forms
    
- same-turn grant rules
    
- membership
    
- exactly three blockers
    
- self-amendment prohibition
    
- occurrence/count/reservation
    
- carry
    
- suspension/end
    
- informed-authorization repair
    
- dependency of execution latitude on Recovery Capability
    

### `recovery-policy.md`

Owns:

- Recovery Capability
    
- admissible Recovery Evidence
    
- per-use application
    
- `BOUNDED / DEMONSTRATED / CURRENTLY APPLICABLE`
    
- composition
    
- Fast
    
- Recovery failure semantics
    
- Capability evidence carry/invalidation rules
    

### `boundary-policy.md`

Owns:

- separately protected target/effect/resource/authority requirement
    
- generic Boundary semantics
    
- small adapters/policies as needed
    

### `release-gate-policy.md`

Owns:

- exact artifact → exact per-effect Target Binding transition
    
- Release preconditions
    
- post-act Release obligations/checks
    
- Release ordering
    
- delivery/deploy validation
    
- unrun-check handling
    

### `work-unit-format.md`

Owns serialization only:

- representation
    
- field encoding
    
- compact rendering
    
- Target Binding reference/properties where representation is needed
    

It owns no policy semantics.

### `SKILL.md`

Thin router only:

- activation
    
- Human compression
    
- short invariant that active context is a candidate until target resolution establishes project context
    
- applicable-policy loading
    
- no duplicated policy semantics
    

---

## 7. Goal resolution

Do not infer the whole Goal.  
Resolve only enough of the Goal to choose the next safe action.

> **Ambiguity is acceptable until it changes the next action.**

Ask only when unresolved ambiguity leaves a materially distinct Human-owned choice.

An inferred Goal must not silently broaden:

- mutation scope
    
- Target
    
- effect
    
- recipient/object
    
- value/count
    
- authority
    
- accepted known-unrecoverability
    

Challenge may question the Goal.  
It must never silently replace it.

Code complete != Delivery complete != Goal achieved.  
Goal achievement requires observable supporting evidence appropriate to the Goal.

---

## 8. Operations

Exactly three Operations exist:

- `CHANGE`
    
- `RESTORE`
    
- `CONTAIN`
    

### CHANGE

Move operative state toward a desired new state in pursuit of the Goal.

### RESTORE

Return an identified restore unit to an identified known-good state.  
Do not improve while restoring.

### CONTAIN

Stop or reduce accumulating harm / propagation or buy time without pretending the underlying Goal or failure has been resolved.  
Contain may intentionally degrade functionality.  
Contain success means harm accumulation stopped, not root cause fixed.

Each Operation is independently classified and authorized.

CONTAIN has no emergency authority.

A clear isolated attributable grant may include ordinary CHANGE plus bounded RESTORE when no material authority choice is invented.  
CONTAIN is never silently included.

---

## 9. Work Unit

Definition:

> **A Work Unit is the smallest state-changing outcome that is independently meaningful enough to classify, authorize, execute, and validate.**

Flat means:

> **No authority inheritance.**

It does not mean no relationships.

Minimum semantic content belongs to `ahl-flow.md` and includes, as applicable:

- identity
    
- Goal reference / Goal contribution
    
- Operation
    
- selected Route
    
- scope
    
- per-effect Target Binding
    
- material effects
    
- exclusions
    
- dependencies / safety-critical ordering
    
- factual AHL Level
    
- Recovery Capability application when relied upon
    
- Boundary requirements/results
    
- Release requirements/results
    
- Authorization Envelope reference/membership result
    
- validation requirements
    
- Route stop conditions
    
- occurrence identity / allowance reservation when required
    

A durable Work Unit artifact is not required for every internal edit.  
Representation may remain in active context unless carry, audit, counting, unresolved discrepancy, Release, or another real requirement needs durability.

### Consequence anti-fragmentation reference

When finalizing Work Unit boundaries and classifying the selected Route, apply the anti-fragmentation rule defined in `consequence-policy.md`.

`ahl-flow.md` / Work Unit semantics define **no separate anti-fragmentation semantics**.

---

## 10. Evidence

Exactly four general Evidence states exist:

- `DECLARED`
    
- `OBSERVED`
    
- `VERIFIED`
    
- `UNEVALUATED`
    

### DECLARED

The proposition has been asserted but is not established by applicable current observation.

### OBSERVED

The proposition is directly supported by admissible, scoped, sufficiently fresh observation.

### VERIFIED

The proposition has been established against the applicable discriminating validation criterion.

### UNEVALUATED

No currently applicable evaluation has established the proposition.

`UNEVALUATED` does not mean false.  
`UNEVALUATED` does not mean low confidence.

Evidence binds an exact proposition with:

- source
    
- scope
    
- observation time / relevant freshness
    
- locator where applicable
    

Do not assign one Evidence state to a whole record when only one proposition was observed.

The states are not a universal confidence ladder.  
Domain policy determines whether `OBSERVED` or `VERIFIED` is sufficient where stronger Evidence is required.

Memory may carry a claim or locator.  
Memory does not raise Evidence state.  
Agent repetition remains DECLARED.

### Narrow default for load-bearing mutable factual propositions

Before a state-changing occurrence may `PROCEED`, an exact **factual** proposition cannot rely on `DECLARED` or `UNEVALUATED` alone when **all** of the following are true:

1. it is load-bearing to occurrence membership or immediate safe execution;
    
2. it is current or materially mutable for that occurrence; and
    
3. if false, a credible material Target, effect, Recovery, Boundary, or Release-integrity escape exists.
    

Obtain the **smallest applicable discriminating read-only Evidence**—`OBSERVED` or `VERIFIED` as the owning policy requires—or return `PREREQUISITE_REQUIRED`.

Reuse still-applicable Evidence.  
Re-observe only after a material-change possibility or an invalidation trigger.

This rule does not convert Human grant/provenance or deterministic Policy derivation into factual Evidence.  
It creates no universal scanner and no observation-on-every-mutation rule.

---

## 11. Load-bearing

A proposition is load-bearing when its truth may materially change:

> **the next action, or an immediate conclusion required to select, authorize, execute, validate, recover, contain, or deliver that action.**

Load-bearing does not mean interesting, uncertain, or merely available to inspect.

AHL observes only what applicable policy requires for the current next-action decision.

This is the open-world limiter.  
It prevents “observe everything” from becoming impossible universal ceremony.

---

## 12. Challenge

Challenge tests premises material to the next safe action.

Challenge may:

- obtain cheap read-only facts
    
- falsify assumptions
    
- expose contradictions
    
- eliminate invalid Routes
    
- establish Target identity
    
- test Recovery/Boundary/Release prerequisites where read-only observation suffices
    

Challenge remains available during:

- Startup
    
- Goal resolution
    
- candidate Route analysis
    
- final semantic fixpoint
    
- occurrence refresh
    
- validation
    
- failure handling
    

Human `stop asking me` does not disable Challenge.

Challenge must remain:

- cheap
    
- mostly silent
    
- non-ceremonial
    

> **AHL should notice without narrating every act of noticing.**

Challenge must not suppress an otherwise-required load-bearing observation because the expected answer is inconvenient to Human or Agent preference.

---

## 13. Arbiter

Arbiter is a rare technical adjudication mechanism inside Challenge.

Use only when:

- at least two materially different legitimate technical Routes remain
    
- Policy cannot mechanically choose
    
- cheap read-only discovery cannot resolve them
    
- legitimate Evidence can rank them
    
- the Human left the technical choice open
    
- Goal, authority, reserved constraints, and effect Envelope remain unchanged
    

Possible outcomes:

- `ROUTE_SELECTED`
    
- `ROUTE_UNDETERMINED`
    

Arbiter operates only inside the choice space left open by attributable Human decisions and established facts.

Arbiter may decide.  
It cannot grant permission.

Arbiter may interpret.  
It cannot invent.

Arbiter must never:

- authorize mutation
    
- invent facts
    
- invent Evidence
    
- invent authority
    
- replace Goal
    
- expand an Envelope
    
- override a materially Human-declared Route
    
- manufacture Recovery applicability
    
- waive Boundary or Release requirements
    
- waive any blocker
    
- decide factual Level
    
- decide Human preference/value/legal/business/ownership questions
    

Broad delegation enlarges Arbiter's legitimate choice space, not its powers.

`ROUTE_UNDETERMINED` is a Challenge outcome before Authorization, not an Authorization blocker.

---

## 14. Core and deterministic Policy

### Core

Core is orchestration only.

Core may:

- manage lifecycle state
    
- manage dependencies/order
    
- apply deterministic reachability
    
- dispatch components
    
- schedule already-authorized work
    
- execute mechanical occurrence reservation/recording where required
    
- re-enter the earliest affected flow phase when a new material fact invalidates downstream conclusions
    

Core must not:

- exercise discretionary Route judgment
    
- invent Goal/facts/Evidence
    
- grant or widen Authorization
    
- waive blockers
    
- decide or downgrade factual Level
    
- silently interpret semantic membership by itself
    
- replace an owner
    

Core must not become Control Tower under another name.

### Policy

Policy owns deterministic rules.

Policy may derive:

- deterministic requirements
    
- blocker predicates
    
- mechanical reachability
    
- domain sufficiency rules for Evidence
    
- mechanical classification constraints
    

Policy must not:

- invent Evidence
    
- exercise discretionary technical judgment
    
- grant mutation permission
    
- replace an owner
    
- decide Human values/preferences
    

---

## 15. Startup Target Resolution

Observed failure class:

> **Mutation-target binding failure.**

Core startup invariant:

> **The active execution context is a candidate, not the target.**

Equivalent:

> **Target is established, not inherited.**

No Target Manager subsystem exists.  
Target identity is Evidence about the existing `Work Unit.target`.

### Per-effect Target Binding

Before each state-changing effect, the Work Unit must have a Target Binding establishing:

- attributable intended role / target constraints / exclusions
    
- observed concrete provider/tool destination that will receive this effect
    
- discriminating Evidence source / locator / freshness
    
- load-bearing mutable target predicates
    
- invalidation triggers
    

The actual tool/provider destination must satisfy the current Target Binding before mutation.

### Required precision

AHL does not require globally unique physical identity.  
It requires enough observed identity that:

1. actual destination satisfies attributable target constraints/exclusions relevant to the effect;
    
2. no unresolved materially non-equivalent candidate remains inside bounded discovery scope;
    
3. load-bearing mutable predicates are fresh enough;
    
4. the occurrence still belongs to the Envelope;
    
5. applicable Boundary requirements are satisfied;
    
6. relied Recovery is applicable to this exact target/application;
    
7. technical reachability for the intended Operation exists.
    

A target alternative is materially non-equivalent when choosing it could change:

- effect
    
- authority
    
- Recovery applicability
    
- Release/delivery outcome
    
- protected Boundary
    
- Human work/state preserved, overwritten, or bypassed
    

If candidates are materially equivalent for this Work Unit, do not manufacture a Human question merely for physical uniqueness.

### Evidence must discriminate

A folder name, branch name, cwd, Agent memory, or a marker shared by all candidates is not target proof by itself.  
Use only discriminating properties load-bearing to the current target kind and Work Unit.

### Bounded discovery

Discovery is read-only and prefers:

1. inherited candidate
    
2. attributable Human/mandate hints
    
3. durable target/provenance descriptors
    
4. host-configured roots / registered workspaces / known endpoints
    
5. direct relevant siblings / known candidate locations
    
6. provider-specific identity observations needed to eliminate candidates
    

Do not perform whole-disk scans, unrelated recursive scans, broad network probing, or broad account/cloud enumeration merely to find a target.

### Discovery must not mutate Human state

During target discovery, do not:

- stash
    
- reset
    
- discard
    
- commit
    
- snapshot
    
- copy
    
- overwrite
    

Human-owned/uncommitted state merely to make rerouting convenient.

Observe it.  
If preserving or handling it requires a real Human-owned choice, ask that one question.

### Attention reroute vs mutation reroute

> **Rerouting attention is read-only discovery.**

> **Rerouting mutation changes Target Binding and is subject to Authorization, Boundary, and Recovery.**

Discovery, credentials, writability, access, and reachability do not create authority.

### Human question rule

Ask only when a residual Human-owned decision remains, including materially distinct legitimate targets, an unobservable Human-only fact, host access/switch action, overlapping Human work decision, separately owned Boundary, or deliberately open value/ownership choice.

Do not ask the Human to verify machine-observable path/HEAD/worktree/provider identity when AHL can safely derive it.

---

## 16. Host bootstrap

A minimal pre-project host bootstrap is required for a **conforming host**, because project-local AHL cannot locate the project before project policy is loaded.

The host bootstrap owns pre-project reachability only:

- inherited context is a candidate
    
- bounded read-only target discovery
    
- unique/materially-equivalent resolution
    
- read-only rebind when host permits
    
- mutation floor until project AHL is established
    
- `unique / multiple / not found / outside capability` result
    
- compatible project-policy loading
    

It must not contain:

- AHL Level policy
    
- Authorization tables
    
- Boundary decisions
    
- Recovery selection
    
- discretionary Route policy
    
- project-specific rules
    

Project-local policy cannot waive the pre-project mutation floor.

If host bootstrap and project policy are startup-safety incompatible, fail closed before mutation.

A host that cannot implement this adapter projection is not conforming for state-changing AHL work; it may still perform read-only assistance.

---

## 17. AHL Level

Exactly four factual consequence levels exist.

### AHL1 — NON-OPERATIVE

Wrong execution changes only non-operative representation and cannot credibly alter meaningful Agent/system behavior, workflow results, authoritative state, consequential Human/user action, or external effects.

Behavior-changing Markdown/policy text is not automatically AHL1 merely because the file extension is documentation-like.

### AHL2 — MINOR

Wrong execution changes meaningful operative behavior or output, but no credible consequence reaches materiality.

### AHL3 — MATERIAL

Wrong execution can materially affect a bounded workflow, authoritative/shared state, coupled units, a real subject, or a limited external/operational outcome, while credible harm remains bounded and non-critical.

AHL3 owns bounded material consequence.

Persistence after revert is an indicator, not the definition.

### AHL4 — CRITICAL

Wrong execution can violate a critical protected invariant or cause broad, severe, or insufficiently bounded material harm.

### Classification rule

Classify the highest credible consequence of the **selected Route in actual context**, including:

- direct effects
    
- intended ordinary consumer effects
    

Exclude speculative remote chains.

Level must not encode:

- Recovery
    
- urgency
    
- effort
    
- confidence
    
- Human preference
    
- permission
    
- Operation
    
- target label
    
- domain ownership
    
- file count
    

Recovery does not lower Level.  
Production does not automatically raise Level.  
Database work does not automatically become AHL4.

### Anti-fragmentation — owned by `consequence-policy.md`

Classification is over coordinated factual consequence, not arbitrary edit slicing.

> **Work Unit decomposition must not lower coordinated consequence.**

When multiple mutations have no independently meaningful outcome and jointly produce one material outcome, classify the coordinated outcome in its combined context.  
Do not emit `N` separately lower-classified Work Units merely to reduce factual Level.  
A materially meaningful AHL4 outcome split into nominal AHL2 edits remains classified by the coordinated outcome.

### Classification actors

- `consequence-policy.md` owns definitions and deterministic classification rules.
    
- The acting Agent applies them to established facts and makes evidence-backed semantic judgment where required.
    
- Challenge obtains/tests load-bearing facts.
    
- Policy mechanically derives only what is mechanically derivable.
    
- Core does not decide Level.
    
- Arbiter does not decide Level.
    

Unknown/missing facts must not be encoded as “low confidence Level.”  
Use the honest highest credible consequence where that is the factual result, or resolve the load-bearing prerequisite before safe act when required.

---

## 18. Human shorthand and grant formation

Human numeric shorthand is input vocabulary, not factual truth.

Delete as canonical concepts:

- Requested Safety Profile
    
- Requested Execution Profile
    
- Applied Safety Profile
    
- Requested AHL numeric field
    
- AHL4-strength profile scale
    

Examples:

### `1で`

May normalize to minimum ceremony and broad **bounded** delegation inside an already attributable work box.  
It never lowers factual Level.

### `4で慎重に`

May add work-specific controls.  
It does not change factual Level.  
It is not mutation approval by itself.

### Same-turn grant

`1で`, `確認いらない`, or `動くまで` may form or complete a same-turn grant only when attributable context already closes Goal, scope, target, material effect class, and material authority choices well enough that the Agent invents none.

A bare task request does not automatically clear material authorization when material choices remain open.

An inferred Goal does not broaden grant scope, Target, effects, or authority.

One-time shorthand does not silently become a durable future preference.

---

## 19. Closed-World Authorization Envelope

Authorization is:

> **The sole determination that a state-changing occurrence belongs to a still-valid authority-granted Closed-World Authorization Envelope.**

A provenance reference and Agent-created Envelope do not form a grant merely by coexisting.

> **The Human or attributable mandate must be attributable to the exact normalized/versioned Envelope.**

Normalization may narrow or clarify directly supported bounds.  
It may add controls.  
It must not silently broaden:

- material scope
    
- Target
    
- effect
    
- recipient/object
    
- value/count
    
- optional-control exception
    
- accepted known-unrecoverable effect
    

Envelope includes, as applicable:

- Goal / completion condition
    
- allowed Operations
    
- scope
    
- Target allowance
    
- material effects
    
- exclusions
    
- Boundaries
    
- recipient/object/value/count limits
    
- accepted known-unrecoverable effects
    
- Recovery dependency reference/subset
    
- controls
    
- permitted optional-control exceptions
    
- Envelope end conditions
    

### Envelope forms

The same Closed-World model may be:

- singleton
    
- finite/bounded
    
- iterative
    
- conditional
    

A conditional Envelope must bind the exact trigger and authorized action/effect.  
This is how pre-authorized CONTAIN can execute without a fresh Human turn when its exact trigger occurs.  
Active harm alone creates no authority.

### Route stop vs Envelope end

> **A Route stop condition stops that Route. An Envelope end condition ends the Authorization Envelope. One does not imply the other.**

A stopped Route must not automatically evaporate a still-valid Human grant.

---

## 20. Authorization blockers

Exactly three canonical Authorization blocker classes exist:

- `APPROVAL_REQUIRED`
    
- `PREREQUISITE_REQUIRED`
    
- `BOUNDARY_REQUIRED`
    

No fourth blocker exists.

`ROUTE_UNDETERMINED` is a Challenge outcome, not an Authorization blocker.

`CONFIRM_REQUIRED` is a compatibility/current-turn surface only.

### APPROVAL_REQUIRED

Use when no valid attributable Envelope covers the occurrence, or the Human/mandate has not granted a required material effect/count/accepted known-unrecoverable effect.

### PREREQUISITE_REQUIRED

Use only when an actual required proposition, Evidence basis, known-good target, Recovery condition, validation basis, or other applicable prerequisite is:

- unestablished under applicable policy
    
- contradicted
    
- unable to satisfy the required prerequisite
    

Agent hesitation alone does not create it.  
Neither does rereading, restating, internal reclassification, confidence change, session change, Agent handoff, or semantically unchanged Route recomputation.

However, if any of those activities exposes a **new objective material fact**—such as a missing requirement, contradiction, Target/effect mismatch, consumed allowance, or Boundary—that fact legitimately invalidates the earliest affected downstream conclusion.

Machine-obtainable prerequisite facts should be established through the smallest safe read-only observation before producing a Human-facing stop.

### BOUNDARY_REQUIRED

Use when a separately protected requirement remains unsatisfied.  
Generic Human approval cannot clear it unless the applicable Boundary owner/policy itself accepts that attributable authority as its satisfaction path.

---

## 21. Authorization membership

A state-changing occurrence may `PROCEED` only while all applicable membership predicates hold:

- Envelope active
    
- Goal open / not completed or revoked
    
- Operation permitted
    
- scope subset
    
- actual per-effect Target/environment is a permitted member/subset of the Envelope allowance
    
- actual material effects subset
    
- exclusions not crossed
    
- recipient/object/value/count in bounds
    
- applicable Boundary satisfied
    
- required preconditions satisfied
    
- relied Recovery currently applicable where execution latitude depends on it
    
- safety-critical ordering prerequisite satisfied and next state-changing step permitted by the current Route
    
- allowance successfully reserved when required
    
- no suspension condition active
    
- no Envelope end condition active
    
- no Route stop condition prevents this occurrence
    

Every occurrence independently matches the same grant.

No authority inheritance exists.  
No self-amendment exists.  
No retroactive legalization exists.

An active Envelope cannot add newly discovered effects to itself, increase its allowance, rewrite history, or legalize work by editing Authorization policy.

---

## 22. Cross-Agent / cross-session carry

Authorization may carry across Agent/session/context changes only when the required basis is preserved and mutable Reality is refreshed.

Carry **must preserve**:

- original attributable Human/mandate provenance
    
- exact normalized/versioned Envelope
    
- applicable policy basis/version/identity needed to interpret that Envelope
    
- current active / suspended / ended state
    
- current occurrence / allowance state where relevant
    

Before use, refresh mutable load-bearing Reality.

The Human's original attributable utterance carried in valid context may serve as provenance.

An Agent summary, paraphrase, or memory alone does not create authority.

A durable carry record is not required for every ordinary internal edit.  
It is required only when the authorization/occurrence state must survive a boundary that ordinary active context cannot safely preserve.

A policy reread, semantically unchanged Route recomputation, restatement, internal reclassification, session change, or Agent handoff does not itself end a still-valid Envelope.

---

## 23. Aggregate consequence and informed authorization repair

Effect semantics are authoritative.

The system derives the Envelope's aggregate factual consequence from permitted effects using consequence-policy semantics.

A Human-selected numeric ceiling is not a substitute for effect semantics.

If the effect Envelope is unchanged but the Human was materially misinformed about aggregate consequence:

1. narrowly suspend affected authorization;
    
2. preserve actual state/effects;
    
3. correct the material representation;
    
4. **reauthorize once**.
    

Reason:

> The Human was materially misinformed.

Not:

> The number changed.

If the Human was already truthfully informed about the aggregate effect box, an internal Work Unit's factual Level changing within that same represented box does not by itself require a new Human turn.

---

## 24. Occurrence identity, allowance, concurrency, retry

Human approval count is not occurrence count.

For accumulating external/material effects:

- track occurrence identity where needed
    
- reserve/consume allowance
    
- timeout/unknown counts as consumed until read-only Evidence establishes non-effect
    
- retry the same occurrence only with real idempotency support
    

For material/critical count/value-limited effects:

> **Successful trustworthy reservation is part of occurrence membership.**

Reservation success and `PROCEED` must be linearized.

> **Core must not dispatch the state-changing occurrence before successful reservation.**

If trustworthy linearization is unavailable:

- serialize execution, or
    
- shrink to singleton authorization
    

Singleton authorization is an Envelope whose permitted count is one, not a second Authorization model.

Do not impose a universal ledger on ordinary internal edits.  
Durable occurrence accounting is required only when actual accumulating effects need to survive retries, concurrency, or carry.

---

## 25. Recovery Capability

Recovery Level does not exist.

A Recovery Capability has exactly seven fields:

1. environment
    
2. restore unit
    
3. restore closure
    
4. mechanism
    
5. validation
    
6. material dependencies
    
7. evidence
    

Do not add an eighth field for per-use application.

### Fast eligibility

Fast credit requires:

> **BOUNDED ∧ DEMONSTRATED ∧ CURRENTLY APPLICABLE**

#### BOUNDED

The actual material effect subset receiving Fast credit fits the demonstrated restore closure and exclusions.

#### DEMONSTRATED

Empirical Evidence supports the mechanism, closure, known-good return, and validation.  
Agent declaration alone is insufficient.

#### CURRENTLY APPLICABLE

Environment, Target/unit, mechanism, exact known-good source, material dependencies, and validation assumptions materially match the carried Evidence.

Recovery Drill is an Evidence-production method, not mandatory ritual.

Evidence may carry only while its material basis remains valid.

### Composition

Capabilities compose automatically only when genuinely independent.

Overlap, ordering, atomicity, shared invariants, coupled state, or other cross-unit dependence requires composite Recovery Evidence.

### Per-use application

A Work Unit's Recovery application binds:

- Capability reference
    
- exact current known-good target/source
    
- actual material-effect subset covered
    
- current applicability result
    

Authorization must make explicit which effect subset, optional-control exception, or execution latitude depends on that Capability.

### Declared-only closure

> **A load-bearing Recovery closure claim that cannot be raised above DECLARED in the current environment receives no Fast credit.**

This alone does not automatically change factual Level or revoke unrelated authorization.  
If the proposition is also load-bearing to membership and a credible escape exists, observe minimally or return the applicable prerequisite result.

### Recovery failure

If execution latitude depended on a Capability and that Capability fails:

- suspend only dependent effect subset / latitude
    
- preserve Human Goal and attributable grant unless their own binding changed
    
- preserve discrepancy/Evidence
    
- investigate read-only
    
- do not use the failed Capability as authority for its own repair
    
- any state-changing repair/proof is a separate Work Unit
    
- CONTAIN requires independent valid authority
    
- re-demonstrate the Recovery basis
    

If the same material binding remains valid after re-demonstration, dependent latitude may resume without repeated Human approval solely because Recovery was repaired.

> **Recovery failure invalidates dependent execution privilege, not Human intent.**

Recovery does not select Target, grant authority, or change factual Level.

---

## 26. Boundary

A Boundary is:

> **A deterministic separately protected requirement created by touching a protected target, effect, resource, or authority.**

Boundary is independent of AHL Level.  
It is satisfied by its applicable policy/owner, not waived by generic approval or technical access.

Credentials, access, discovery, writability, Recovery, and Level do not automatically satisfy Boundary.

Use one generic model with small adapters where needed.  
Do not create a giant domain taxonomy.

Boundary failure is local/narrow.  
It does not create a generic global degraded Mode.

Canonical blocker name:

- `BOUNDARY_REQUIRED`
    

---

## 27. Release and temporal requirements

Release is independent from Boundary and Authorization.

`release-gate-policy.md` owns:

- exact artifact → exact per-effect Target Binding transition
    
- release-specific prerequisites
    
- required checks
    
- unrun-check handling
    
- release ordering
    
- release/deploy validation
    

Release Gate never grants mutation permission.

Responsibility split:

- **Boundary:** what separately protected requirement applies and whether it is satisfied.
    
- **Release:** what evidence, ordering, pre/post checks are required for this artifact → target transition.
    
- **Authorization:** whether this exact occurrence belongs to a valid Envelope.
    

### Precondition

Must be satisfied before `PROCEED`.

Examples include required authority, artifact identity, pre-deploy check, or Evidence needed for membership.

### Post-act obligation

Before act:

- its plan must be known
    
- its reachability must be established/bound as required
    

After act:

- actual discriminating Evidence is required for completion
    

Do not make a logically post-act observation an impossible precondition.

`unrun`, `unknown`, or `not yet observed` is not PASS.

---

## 28. Route lifecycle and Route Adherence

Route decision is required for state-changing work.  
Route presentation and persistence are conditional and risk/context dependent.

A Route binds only safety-critical ordering and state-changing constraints necessary to keep the selected execution path safe.

Do not freeze ordinary independent read-only discovery order merely for ceremony.

Before each state-changing occurrence:

- refresh applicable safety-critical ordering prerequisites
    
- confirm the occurrence is the next state-changing step currently permitted by the selected Route
    
- confirm current Target Binding and Authorization membership still hold
    

If new Evidence materially changes the safe Route, revise/select the Route **before** the next mutation.

### Route violation

If actual execution violates the bound safety-critical Route:

1. stop additional mutation;
    
2. preserve the actual changed state and Evidence;
    
3. expose into the active decision path:
    
    - Expected Route / required ordering
        
    - Actual execution
        
    - observed changed state;
        
4. do not create a post-hoc savepoint/snapshot/recovery artifact and claim the prior prerequisite was satisfied;
    
5. do not rewrite Route history to legalize the already-occurred mutation;
    
6. do not retroactively expand Authorization;
    
7. begin repair only through a newly valid Work Unit / Route / Authorization path as applicable.
    

A Route violation is not erased by editing the Route after the fact.

A Route stop condition stops the Route, not automatically the Envelope.

---

## 29. Candidate phase and final semantic fixpoint

### Candidate phase

Before Route selection, Challenge / Policy / Arbiter may provisionally evaluate candidates for:

- effects
    
- consequence range
    
- Recovery applicability
    
- Boundary requirements
    
- Release requirements
    
- Target predicates
    

These are ranking/elimination aids only.  
They are not final Level, final Work Unit, final Recovery application, final Boundary/Release result, Authorization, or mutation permission.

### Final phase

After exactly one selected Route and final Work Unit exist, establish a bounded semantic fixpoint:

1. final per-effect Target Binding
    
2. final factual AHL classification
    
3. independently derived Boundary requirements
    
4. independently derived Release requirements
    
5. Recovery / Evidence prerequisites and exact per-use application
    
6. construct or match a Closed-World Authorization Envelope
    
7. derive aggregate consequence from effect semantics
    
8. perform informed-authorization repair if required
    
9. test occurrence membership
    

If a **new material fact** appears, re-enter the earliest affected final step and invalidate/recompute all downstream conclusions that depend on it.

A reread, restatement, internal reclassification, confidence change, or unchanged Route recomputation is not itself a new material fact.

Non-convergence does not loop forever.  
Dispatch by cause:

- unresolved technical Route → `ROUTE_UNDETERMINED`
    
- objective prerequisite unestablished/contradicted → `PREREQUISITE_REQUIRED`
    
- valid attributable Envelope absent → `APPROVAL_REQUIRED`
    
- separately protected requirement unsatisfied → `BOUNDARY_REQUIRED`
    

Target/project-context invalidation returns to Startup Phase 0.

---

## 30. Delta-scoped occurrence refresh

Before each mutation:

> **Refresh only mutable load-bearing predicates whose truth may have changed.**

Occurrence refresh is not full reevaluation.

Reuse unchanged:

- Policy
    
- established Evidence basis
    
- Envelope
    
- Target Binding
    
- context
    

Do not automatically repeat:

- full policy load
    
- full Goal analysis
    
- full classification
    
- full Recovery analysis
    
- full Target resolution
    
- Human approval
    

unless a new load-bearing fact or material reference change requires the affected step.

---

## 31. `CONFIRM_REQUIRED`

Where a legacy/compatibility surface still emits `CONFIRM_REQUIRED`:

- the current turn ends
    
- no mutation occurs later in that same turn
    

`CONFIRM_REQUIRED` is not a fourth blocker.

On the next turn, re-evaluate affected predicates using carried attributable grant/Evidence/current Reality.  
Do not recreate approval merely because the previous turn ended or the same trigger remains syntactically applicable.

---

## 32. Act, Validate, failure Work Units, Goal check

Once all applicable membership and prerequisites are satisfied:

```
PROCEED
→ Act
→ post-act obligations
→ Validate
→ Goal check
```

Failure does not create a special Mode.

A failure creates another Work Unit as appropriate:

- CHANGE
    
- RESTORE
    
- CONTAIN
    

Each is independently classified and authorized.

Validation must not report an unrun/unknown check as PASS.

Code complete != Delivery complete != Goal achieved.

---

## 33. Policy loading

Before project-local state-changing work:

- host bootstrap / target resolution only
    

After correct project context is established, load the minimal required live semantics.

For state-changing work, core flow / consequence / Authorization are generally load-bearing.  
Load Recovery only when relied upon or materially evaluated.  
Load Boundary only when a protected target/effect/authority may apply.  
Load Release only for release transitions.  
Load serialization only when durable/carry/audit/count representation is actually required.

`ahl-flow.md` is the sole normative owner of policy-basis identity/version semantics for loading, reuse, and Authorization carry.

A policy basis must expose a stable identity/version sufficient to determine whether its load-bearing semantics materially changed. The concrete identity/version mechanism is provider-independent; Git, GitHub, or any particular versioning system is not required.

A policy reread alone does not invalidate unchanged Authorization. A material policy-basis change invalidates the earliest affected downstream conclusions and requires reevaluation only from that point.

Do not full-reread unchanged policy on every mutation.

Do not turn Challenge into narrated ceremony.

---

## 34. Human understanding and Human-interface guidance

Human understanding is not directly observable.

AHL does not need to prove that the Human “understood.”

Human authority/provenance and factual Evidence remain distinct.  
An interaction does not become factual Evidence merely because it occurred.

The Kernel must not require pretending that Human comprehension has been established.

UI/affordance guidance such as:

> **Do not present an impossible action as executable.**

belongs in later Human-interface guidance unless it instantiates an existing factual/authority invariant.

No comprehension manager or new Kernel object is introduced.

---

## 35. Known residual risks

AHL must record unresolved limits rather than silently convert them into certainty.

### Recovery closure integrity

AHL cannot prove a Recovery closure merely because its own declaration says the closure is complete.  
A poorly declared closure can omit effects and thereby attempt to purchase unearned Fast execution.

Mitigations include:

- proposition-scoped Evidence
    
- discriminating observation
    
- explicit exclusions
    
- discrepancy preservation
    
- declared-only closure receives no Fast credit
    
- Recovery applicability invalidates on material basis change
    
- external/irreversible escapes remain protected by applicable Boundary/Release semantics
    

These are mitigations, not a proof that no omitted effect exists in an open world.

### Opaque dependency drift

A carried Recovery demonstration can become stale through unobserved dependency drift such as expired credentials, unreachable storage, platform changes, or corruption.  
Material-basis invalidation and low-cost observation/sampling may be required by applicable domain policy where the dependency can drift invisibly.  
Do not replace this with universal periodic ceremony.

### Unexplained discrepancy

An unexplained material difference must remain visible.  
Do not normalize it away merely to complete validation or make the result look clean.

> **Known residual risk is recorded, not silently promoted to certainty.**

---

## 36. Legacy AHL status

> **Legacy AHL is migration input, not a supported parallel architecture.**

> **Preserve the contract, not the legacy implementation.**

> **旧AHLは守らない。旧AHLが守っていたものだけ守る。**

Legacy AHL has completed its role as:

- prototype
    
- field-test implementation
    
- failure-discovery instrument
    
- source of historical safety contracts
    

Legacy receives no new design except an urgent safety repair required while it remains live.

Do not:

- modernize legacy terminology
    
- optimize legacy Tax
    
- migrate newborn concepts into legacy structure
    
- clean up AHL5/AHL6 as a permanent model
    
- make legacy platform-independent
    
- redesign legacy Recovery
    
- maintain old and newborn architectures in parallel
    

Read legacy only to extract still-required contracts, convert them into newborn semantics and Sentinels, then retire the superseded owner.

---

## 37. Legacy ordinal contract extraction

Do not numerically map:

```
AHL5 → AHL4
AHL6 → AHL4
```

Legacy ordinal constructs are historical compressed contracts, not newborn semantics.

Inventory every active ordinal consumer and extract what it actually protected, including at least:

- `AHL2–AHL6`
    
- `AHL4+`
    
- requested-vs-estimated comparisons
    
- higher requested profiles
    
- legacy AHL1 fast path
    
- “choose the higher level”
    
- AHL5 urgency behavior
    
- AHL6 Recovery behavior
    
- legacy DB AHL4 floor
    

Re-express each protection through newborn owners such as:

- Consequence
    
- Route/context
    
- Operation
    
- Target Binding
    
- Recovery
    
- Boundary
    
- Release
    
- Authorization
    

Historical Scenario 3 and relevant AHL5/AHL6 cases become Sentinels.

The old ordinal implementation itself is not preserved as architecture.

If a transitional live predicate must remain during cutover, it must be semantically non-narrowing until the newborn replacement owner is active.  
Do not remove the legacy DB safety floor before the newborn DB Boundary path is actually routed and active.

---

## 38. Newborn implementation staging

Newborn canonical files may be drafted and audited **without becoming live policy**.

Do not create a live mixed newborn/legacy policy graph.

The newborn graph must exist coherently before activation:

```
ahl-flow
consequence-policy
authorization-policy
recovery-policy
boundary-policy
release-gate-policy
work-unit-format
SKILL/router
host/project entry routing
```

Drafting order is an implementation concern.  
Activation is a system transition.

---

## 39. Quiescent atomic cutover

Preferred migration principle:

> **Do not carry ambiguous live legacy execution state across the semantic cutover when it can be safely quiesced instead.**

Before activating newborn semantics:

1. stop dispatch of new legacy state-changing occurrences;
    
2. quiesce or explicitly resolve in-flight occurrences;
    
3. preserve/resolve unknown-result occurrence state and consumed allowance;
    
4. preserve any real reservation/occurrence accounting that must not double-execute;
    
5. ensure newborn owners/router/entry path are coherent;
    
6. ensure required legacy contracts are represented in newborn semantics and Sentinels;
    
7. establish an execution barrier/fence so no Agent can dispatch under the wrong side of the cutover;
    
8. activate newborn routing atomically from the execution system's perspective;
    
9. remove superseded legacy owners promptly;
    
10. resume state-changing work under newborn semantics only.
    

### Legacy Authorization carry across cutover

**Default: do not carry legacy approval across the architecture cutover when quiescence permits a clean restart.**

If a specific live obligation cannot safely be quiesced and Authorization state must migrate, migration is allowed only when original provenance, scope, Target, effects, counts, and relevant state are reconstructable without inference.

Any migrated legacy approval becomes at most an exact/narrow/singleton newborn Envelope sufficient for that already-bounded obligation.

Never infer broad delegation from legacy state.  
Never map legacy numeric level/profile to mutation authority.

### Activation itself

The activation/cutover is a state-changing Work Unit governed by the **currently live pre-cutover policy** until the activation boundary is crossed.  
Its Target, Route/order, Recovery, Boundary, Authorization, and validation must be established under that live policy.

Historical records are not rewritten to pretend the past used newborn semantics.

---

## 40. Legacy retirement gate

Double-audit PASS of this architecture target authorizes **newborn implementation**, not immediate deletion of the live legacy AHL.

Legacy deletion occurs only when:

1. newborn canonical owners exist;
    
2. newborn router / entry path exists;
    
3. no required live semantic owner points to legacy;
    
4. still-required legacy safety contracts are mapped to newborn semantics;
    
5. required historical Sentinels exist;
    
6. newborn policy graph passes internal audit;
    
7. cutover can occur without a live hybrid graph;
    
8. in-flight / occurrence / allowance state is quiesced or explicitly migrated safely;
    
9. the cutover Work Unit itself is authorized and validated.
    

Then:

> **Cut over and retire superseded legacy owners immediately.**

Do not maintain a long compatibility tail.  
No fallback silently reads legacy semantics after cutover.

---

## 41. High-value Sentinel contract

Legacy experience survives as tests, not architecture.

At minimum the newborn design must support discriminating Sentinels for:

1. README typo: AHL1, zero extra Human turn.
    
2. Behavior-changing policy Markdown: not automatically AHL1.
    
3. AHL2 minor / AHL3 bounded material / AHL4 critical triad.
    
4. `4で慎重に` on AHL2: controls only; no Level change or approval creation.
    
5. Clear `1で、確認不要` in isolated bounded work: same-turn grant; factual Level unchanged.
    
6. Perfect Recovery on critical work: factual Level remains AHL4.
    
7. DB/production: no automatic domain Level floor.
    
8. Broad Envelope: edit/test/fail/RESTORE loop with zero repeated Human approval.
    
9. Internal Route variation inside box: no reauth; safety-critical ordering still enforced.
    
10. Route violation: mutation stops; Expected/Actual/changed state preserved; no retroactive Route legalization.
    
11. Wrong presented aggregate: narrow suspend/correct/reauthorize once.
    
12. Hidden external effect / declaration integrity: no Fast from declaration alone.
    
13. Recovery failure: local suspension; same basis re-demonstrated resumes without reapproval.
    
14. Three pre-authorized external effects: timeout consumes allowance; extra occurrence blocked; no blind retry without idempotency.
    
15. Cross-Agent carry: original provenance + exact Envelope works; summary-only fails.
    
16. Stale carry after suspension/end/consumed allowance fails membership.
    
17. Self-amendment denied.
    
18. Arbiter technical choice allowed; Human value/owner choice returns `ROUTE_UNDETERMINED`.
    
19. Pre-authorized CONTAIN: exact trigger/action only; active harm creates no authority.
    
20. Candidate/final phase: provisional values rank only; exactly one final Work Unit/Level after selection.
    
21. Requirement temporal phase: post-act check is not fake pre-PASS; unrun/unknown is not PASS.
    
22. Per-use Recovery: generic Capability + wrong current source/Target earns no Fast.
    
23. Recovery composition: coupled units without composite Evidence do not inherit Fast automatically.
    
24. Count race: two Agents race for final allowance; exactly one successful reservation/dispatch.
    
25. Provider outage: exact provider-dependent work stops locally; unrelated work continues.
    
26. Hidden Tax: repeated edits/restores inside unchanged Envelope → zero repeated approval, zero full-reference rereads, zero per-edit artifacts.
    
27. Route stop vs Envelope end: stopped Route does not automatically kill grant.
    
28. Wrong same-name workspace: correct Target found read-only; wrong workspace remains unmodified.
    
29. Two materially distinct legitimate targets: zero mutation; exactly one narrow Human decision.
    
30. Correct Target outside host capability: exact Target identified; only switch/access action requested.
    
31. Discovery encounters Human-owned uncommitted state: no stash/reset/discard/commit/snapshot/copy/overwrite.
    
32. No-Git target resolution succeeds without mandatory Git marker.
    
33. Non-discriminating marker does not establish Target identity.
    
34. Materially equivalent Targets do not create Human selection Tax.
    
35. Recovery A → reroute B invalidates per-use Recovery until re-evaluated.
    
36. Artifact correct / destination wrong: Release stops before mutation.
    
37. Policy reread / unchanged Route recompute does not evaporate Authorization.
    
38. Agent hesitation alone does not create `PREREQUISITE_REQUIRED`.
    
39. New objective fact discovered during reread correctly re-enters earliest affected step.
    
40. Inconvenient observation avoidance: required load-bearing observation is not skipped because the result may be unwelcome.
    
41. Material premise/Evidence contradiction is exposed into active decision path before relying on either preferred account.
    
42. AHL5/AHL6 historical protections are represented by newborn semantics without numeric mapping.
    
43. Atomic cutover: no occurrence dispatches through a mixed newborn/legacy graph.
    
44. Cutover with legacy in-flight state: quiescence or explicit narrow migration prevents duplicate/unauthorized occurrence.
    
45. Human-understanding assumption: presentation/interaction is not silently treated as factual comprehension Evidence.
    
46. Anti-fragmentation laundering: multiple mutations with no independently meaningful outcome jointly create one bounded, non-critical material consequence; finalization classifies the coordinated outcome as AHL3 and does not emit `N × AHL2` Work Units.
    

Sentinels preserve scars.  
They do not preserve obsolete anatomy.

---

## 42. Canonical writing contract

After this architecture target passes independent double audit and is frozen:

- do not redesign during canonical writing;
    
- do not add new architecture objects unless the target is internally impossible without one; if so, stop and report the contradiction;
    
- do not reopen fixed Human decisions;
    
- do not preserve conflicting legacy semantics merely for compatibility;
    
- do not make Git/GitHub/CI/Guard/snapshot a Kernel requirement;
    
- do not duplicate normative ownership across runtime files;
    
- do not make Human UX carry internal schemas;
    
- do not optimize safety by making ordinary work unusable;
    
- do not optimize speed by pretending missing facts, Recovery, Target identity, Boundary satisfaction, or authority exist;
    
- do not let Agent memory become fake Evidence or authority;
    
- do let modern Agent context reduce unnecessary artifact/reread Tax;
    
- do not modify legacy AHL merely to make it aesthetically resemble newborn semantics;
    
- change only the requested canonical owner unless the Human explicitly broadens scope or atomic cutover requires one coherent multi-file activation unit;
    
- report unresolved conflicts;
    
- stop after verification.
    

---

## 43. Human-interface target

The Human should be able to say things such as:

```
1で
確認いらない
壊れたら戻して
これ違う
じゃGo
```

AHL performs the precision behind the interface.

AHL complexity belongs behind the Human interface.  
Human shorthand is input, not truth.  
The Human need not learn Kernel vocabulary to receive Kernel guarantees.

Ordinary AHL Human-visible utterances should be short.  
A stop should communicate the material reason/choice, not dump internal schemas or blocker IDs unless debugging/audit requires them.

---

## 44. End state

The newborn AHL is not:

- a checklist
    
- a permission bureaucracy
    
- a Git workflow
    
- a Recovery product
    
- a classification system
    
- an Agent governor
    
- an agreement-forcing layer
    

It is the Layer that allows Human intent and Agent capability to interact at high speed **without silently sacrificing Goal, Reality, Authority, Target, Boundary, Release integrity, or relied recoverability**.

It does not force premature agreement.  
It preserves load-bearing disagreement long enough to collide with Reality.

Its strictness is concentrated where failure becomes material.  
Everywhere else it gets out of the way.

> **Human grants breadth. Recovery grants speed.**

> **Dangerous boundaries are extremely hard. Everything else is almost transparent.**

---

## 45. Freeze decision — completed

Current status:

> **NEWBORN BLUEPRINT FROZEN**

`PASS_FREEZE — final narrow freeze audit completed; findings NONE.`

The converged Opus/Sol architecture findings and the final Sol pinpoint decisions on Belief delta, Evidence sufficiency, and anti-fragmentation ownership are incorporated in this revision.

Final freeze-gate outcomes:

- `PASS_FREEZE` → mark this architecture target **NEWBORN BLUEPRINT FROZEN** and begin newborn canonical implementation in non-live/staged form.
    
- `NARROW_FIX_REQUIRED` → incorporate only the smallest load-bearing correction and rerun a narrow freeze audit.
    
- `MODEL_REVISION_REQUIRED` → stop implementation and return to architecture discussion.
    

Freeze does **not** itself delete legacy AHL.  
It authorizes newborn implementation.  
Legacy retirement follows §§38–40 after coherent implementation, Sentinels, and quiescent atomic cutover readiness.
