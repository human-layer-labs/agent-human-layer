---
name: agent-human-layer
description: Thin newborn activation and policy-routing layer for Human-facing AHL work.
---

# NEWBORN AHL ROUTER — LIVE RUNTIME AUTHORITY

Status: `NEWBORN AHL — LIVE`

This file is the live activation and routing layer only. It routes applicable
work into the canonical newborn graph through the seven policy owners. It does
not define their policy semantics, duplicate ownership, or create a fallback
or dual ownership between canonical and superseded AHL.

## Entry contract

Before any state-changing action, preserve this invariant:

> The active execution context is a candidate, not the Target.

Route target establishment, Target Binding, target discovery, material
equivalence, bootstrap, drift, and re-entry semantics to
[`ahl-flow.md`](./references/ahl-flow.md). Cwd, an open folder, repository
path, provider endpoint, writable context, credentials, or reachability is not
authority merely because it is active or available.

Human shorthand is input, not truth. Infer only enough intent and Goal to
choose the next safe action. Do not require the Human to provide a factual AHL
Level. Do not adapt Reality to Human preference; infer intent, adapt
presentation, and preserve the facts and owner results that govern the action.

## Smallest applicable owner set

Route the work to the smallest applicable normative owner set. A policy is not
loaded merely because AHL is active, and unchanged policy is not reread as a
universal ritual. Reuse still-valid policy basis and Authorization according
to `ahl-flow.md`; its policy-basis identity/version semantics remain solely
flow-owned.

The normative owners are:

- [`ahl-flow.md`](./references/ahl-flow.md) — lifecycle/orchestration, Work
  Unit semantics, Operations, general Evidence, Goal, Challenge, Arbiter,
  Core, Route, Target/startup, policy loading/reuse, Act, Validate, failure,
  and Reality collision;
- [`consequence-policy.md`](./references/consequence-policy.md) — factual
  AHL1–AHL4 consequence, classification, aggregate consequence, and
  anti-fragmentation;
- [`authorization-policy.md`](./references/authorization-policy.md) — the
  Closed-World Authorization Envelope, grant, membership, blockers, carry,
  suspension/end, occurrence, allowance, and reservation authorization;
- [`recovery-policy.md`](./references/recovery-policy.md) — Recovery
  Capability, Fast qualification, applicability, composition, and Recovery
  failure;
- [`boundary-policy.md`](./references/boundary-policy.md) — separately
  protected Boundary requirements and Boundary satisfaction;
- [`release-gate-policy.md`](./references/release-gate-policy.md) — artifact
  to Target release transition, release prerequisites, checks, ordering, and
  validation; and
- [`work-unit-format.md`](./references/work-unit-format.md) — serialization
  only when a structured or durable Work Unit representation is actually
  required.

These are routing references, not duplicated policy definitions. The owner
files remain the sole normative source for their named concepts.

## Conditional loading

For read-only or otherwise non-state-changing work, do not automatically load
the mutation policy graph. Load only the references required by the actual
next action.

For state-changing work, route through [`ahl-flow.md`](./references/ahl-flow.md)
and load the following only when applicable:

- load [`consequence-policy.md`](./references/consequence-policy.md) when
  factual consequence classification is required;
- load [`authorization-policy.md`](./references/authorization-policy.md) when
  Authorization, grant, membership, carry, reservation, suspension, or end
  is required;
- load [`recovery-policy.md`](./references/recovery-policy.md) when Recovery
  capability, applicability, latitude, prerequisite, failure, or restore
  reasoning materially participates;
- load [`boundary-policy.md`](./references/boundary-policy.md) when a
  separately protected requirement may affect the occurrence or membership;
- load [`release-gate-policy.md`](./references/release-gate-policy.md) for an
  artifact/state transition governed by Release Gate; and
- load [`work-unit-format.md`](./references/work-unit-format.md) only when
  structured or durable Work Unit serialization is actually required.

Conditional loading reduces unnecessary policy Tax. It never skips an
applicable owner or weakens a required prerequisite. If an applicable owner
cannot be loaded or a required prerequisite cannot be established, route to
that owner's failure or blocker semantics. Do not silently satisfy the
missing requirement or create a global degraded mode; unrelated Work Units
may continue when their own owners and prerequisites remain valid.

## Human-facing compression

Keep ordinary interaction short. The Human need not operate AHL internals
manually, repeat an unchanged factual description, or repeatedly reconfirm an
unchanged valid Authorization Envelope that already covers the occurrence.
Ask only when an actual Human-owned decision or unresolved authority choice
remains. Surface a blocker or consequential choice when it changes the next
action; do not hide Reality behind compressed presentation.

`CONFIRM_REQUIRED` remains flow-owned compatibility/current-turn behavior. A
policy reread alone does not evaporate unchanged Authorization, and full
policy reread before every mutation is not required. These statements route
interaction to the owners; they do not redefine Authorization, Evidence,
Route, or policy-basis semantics here.

## Router boundaries

This file must not define or duplicate factual levels, classification,
anti-fragmentation, Envelope structure, grant formation, membership,
blockers, Recovery fields or Fast qualification, Boundary derivation or
satisfaction, Release semantics, Work Unit serialization, Evidence states,
Target Binding, Route violations, Arbiter jurisdiction, or policy-basis
identity semantics. It names those concepts only to route them to their
normative owners.

The router is provider-independent. It does not require Git, GitHub, pull
requests, CI, snapshots, a particular IDE, or a particular Agent host.
Provider integrations may satisfy owner-defined requirements, but no provider
defines AHL.

The newborn graph is live through this router. Do not turn this router into a
normative owner or add fallback semantics to superseded legacy owners.
