# NEWBORN BOUNDARY POLICY — NON-LIVE STAGING

Status: `NEWBORN IMPLEMENTATION — STAGED, NOT LIVE`

This document is the sole owner of Boundary derivation, separately protected
requirement semantics, and Boundary satisfaction. It is not a runtime
authority and does not activate the newborn graph.

## Ownership boundary

Boundary is an independent requirement dimension. This policy does not define
factual Level, Authorization, Recovery Capability, Target Binding, Release,
Work Unit semantics, or serialization. It supplies a bounded requirement and
satisfaction result for Authorization to consume.

## What Boundary means

A Boundary exists when the protected target, material effect, resource, or
authority touched by a Work Unit creates a separately protected requirement.
The requirement is derived from the actual protected thing and intended
effect, not from the convenience of the route or the technical mechanism.

The generic Boundary result identifies, at minimum:

- the protected target, effect, resource, or authority;
- the separately protected requirement created by touching it;
- the evidence or condition that would satisfy that requirement; and
- the local failure and affected scope if satisfaction is absent.

Boundary derivation is independent of Level. A low factual Level may still
touch a separately protected resource, and a high factual Level does not by
itself prove that a particular Boundary is satisfied.

## DB/production protected-condition adapter

This section is the concrete domain adapter for the load-bearing protection
that the legacy AHL expressed through its numeric DB/schema/production safety
floor and separate DB/live-data protected gate. It replaces that protection;
it does not preserve a numeric Level floor and it does not create a new
normative owner.

### Applicability

The adapter returns `APPLICABLE` only when the final per-effect Target
Binding and material effect facts establish either of these protected
conditions:

1. the Operation state-changes production/live-data database state; or
2. the Operation changes schema/migration state whose application affects
   production/live-data database state.

The factual applicability inputs are, as applicable, the established Target
Binding, the production/live-data database fact, the exact resource/schema or
migration affected, the exact material effect and Operation, and the current
mutable facts required by the normal Evidence rules. A path, branch,
provider, credential, environment label, or technical reachability does not
establish applicability. If neither condition is established, return
`NOT_APPLICABLE` and create no Boundary ceremony.

### Concrete requirement

For an applicable effect, derive the exact requirement
`DB_PRODUCTION_EXACT_AUTHORITY`:

- `protected_target`: the verified Target Binding identity;
- `protected_resource`: the exact production/live-data database resource,
  schema, or migration domain;
- `protected_effect`: the exact material state-changing effect and Operation;
- `factual_basis`: established Target/effect/current-state facts required to
  determine the applicable protected resource; and
- `authority_coverage`: attributable Human mandate or Authorization Envelope
  coverage that explicitly includes the exact protected target, resource, and
  material state-changing effect.

The Human grant or mandate remains authority provenance. It is not relabeled
as `OBSERVED` or `VERIFIED` factual Evidence. Factual Target/effect/current-
state propositions remain governed by the normal Evidence semantics, while
`authority_coverage` is the attributable authority input to this adapter.
Generic permission is not `authority_coverage`.

### Satisfaction and Authorization result

The requirement is `SATISFIED` only when both channels hold:

1. the factual applicability, Target, resource, and effect facts are
   established under the normal Evidence rules; and
2. `authority_coverage` is attributable and explicitly covers the exact
   protected DB target, resource, material effect, and state-changing
   Operation.

An already-valid attributable Human mandate or Authorization Envelope may
satisfy `authority_coverage` when its exact target/effect coverage is already
established. The adapter must not request a second confirmation merely
because it evaluates that same authority. Broader or generic authority that
does not cover the exact protected target/effect is insufficient.

If the condition is `APPLICABLE` and either channel is absent or insufficient,
return `BOUNDARY_REQUIRED` for the affected occurrence/effect subset. If both
channels hold, return `SATISFIED`; the Boundary itself no longer blocks, and
ordinary Authorization membership plus every other applicable prerequisite
continues. If the condition is `NOT_APPLICABLE`, return no Boundary blocker.

Credentials, DB access, writability, connectivity, production access,
Recovery availability, factual Level, and generic Human approval do not
establish `authority_coverage` and do not satisfy this requirement.

This adapter never selects a factual Level. DB involvement does not
automatically create AHL3 or AHL4. Production involvement does not
automatically create AHL3 or AHL4. Schema/migration involvement does not
create a Level floor. `consequence-policy.md` independently classifies the
highest credible consequence of the selected Route in the actual context.

## Derivation and consumption

The applicable owner or policy adapter derives whether a Boundary is present
from the concrete protected target, effect, resource, or authority. It then
returns a requirement and a satisfaction result that are traceable to that
derivation.

When present, `BOUNDARY_REQUIRED` is an authorization input. Authorization
consumes the result and decides whether the bound action may proceed. Boundary
does not grant permission, select an actor, create an Auth Envelope, or
substitute for approval.

## Satisfaction semantics

Credentials, technical access, discovery, writability, reachability, and
Recovery availability do not automatically satisfy Boundary. Neither do:

- the factual Level by itself;
- a generic Human approval not bound to this Boundary and action;
- the existence of a provider, repository, branch, path, environment label,
  or other non-discriminating marker; or
- an assertion that a check was or will be performed without its required
  Evidence.

Satisfaction must match the exact requirement, target, effect, resource, and
authority in scope. An unrun, unknown, stale, or inapplicable factual basis is
not a passing satisfaction result. An attributable authority input must not be
converted into factual Evidence. If the requirement does not exist for the
exact use, the result should say so rather than inventing a generic gate.

## Local failure

Boundary failure is narrow and local to the protected requirement and the
dependent Work Unit or effect subset. It does not create a global degraded
mode, silently widen a blocker, or suspend unrelated Work Units whose own
requirements remain satisfied.

The failure result exposes the unsatisfied requirement, affected scope,
missing or stale basis, and any safe next decision owned by Authorization.
Boundary does not self-authorize repair or make an unrelated action depend on
the failed boundary.

## Provider-independent adapters

The newborn model is provider-independent. A small adapter may translate a
provider's concrete protected resource or authority into the generic Boundary
model and back into provider-specific observations. The adapter must preserve
identity, scope, requirement, satisfaction, and failure semantics.

Git, GitHub, databases, production providers, credentials, and deployment
systems are not canonical Boundary architecture. Their presence can be an
input to an adapter when actually in scope; it cannot redefine the generic
model or make provider presence equal to satisfaction.

## Cross-owner invariants

Boundary is not Level, Authorization, Recovery, Release, Target Binding,
Evidence generally, or Work Unit serialization. Authorization owns permission
and gate decisions; Recovery owns Recovery Evidence; Release owns release
transition requirements; the flow owns Work Unit semantics. References to
those results are allowed, but a reference must not duplicate or replace the
owning rule.

Any document that derives Boundary from credentials alone, conflates Boundary
with factual Level or Authorization, or defines a provider-specific canonical
architecture is an ownership collision and must stop the route for review.
