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
that the legacy AHL expressed through its database minimum floor and separate
DB/live-data/production boundary route. It replaces that protection; it does
not preserve a numeric Level floor and it does not create a new normative
owner.

### Applicability

The adapter returns `APPLICABLE` only when the final per-effect Target
Binding and material effect facts establish one of these protected
conditions:

1. the effect changes an actual database schema definition or runs a database
   migration;
2. the effect mutates live database or live data; or
3. the effect changes a verified production-serving or production-deployed
   target state.

The condition must come from the bound target, resource, and intended effect.
The words `database`, `DB`, `live`, or `production` in a path, branch,
provider, credential, or environment label are not sufficient by themselves.
If none of the three conditions is established, the adapter returns
`NOT_APPLICABLE` and creates no Boundary ceremony.

### Concrete requirement

For an applicable effect, derive one exact protected requirement with these
fields:

- `protected_target`: the verified Target Binding identity;
- `protected_resource`: the exact schema, database, live-data, or
  production-serving resource domain;
- `protected_effect`: the exact material effect subset and Operation;
- `protected_authority`: the separately protected DB/production boundary
  authority or control named by attributable project policy; and
- `required_evidence`: current Evidence that proves that exact target,
  resource, effect, and authority are protected for this occurrence.

The requirement is not a generic request for approval or access. For a
production release transition, an exact applicable Release result may be
part of `required_evidence`; Release remains the sole owner of release
derivation and temporal release checks. This adapter does not duplicate or
replace Release.

### Satisfaction and Authorization result

The requirement is `SATISFIED` only when `required_evidence` is current and
directly establishes the exact `protected_target`, `protected_resource`,
`protected_effect`, and `protected_authority` for the occurrence. The evidence
must be an actual verified boundary result or an exact owner result explicitly
accepted for that requirement. Credentials, DB access, writability,
connectivity, production access, Recovery availability, a factual Level, or
generic Human approval do not satisfy it.

If the condition is `APPLICABLE` and the exact requirement is not satisfied,
return `BOUNDARY_REQUIRED` for the affected occurrence/effect subset. If it
is satisfied, return the Boundary result to Authorization and let ordinary
Authorization evaluation continue. If it is `NOT_APPLICABLE`, return no
Boundary blocker.

This adapter never selects a factual Level. DB involvement does not automatically create AHL3 or AHL4. Production involvement does not automatically create AHL3 or AHL4. `consequence-policy.md` independently classifies the highest credible consequence of the selected Route in the actual context.

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
authority in scope. An unrun, unknown, stale, or inapplicable basis is not a
passing satisfaction result. If the requirement does not exist for the exact
use, the result should say so rather than inventing a generic gate.

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
