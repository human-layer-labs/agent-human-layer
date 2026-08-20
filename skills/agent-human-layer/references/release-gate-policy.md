# NEWBORN RELEASE GATE POLICY — LIVE

Status: `NEWBORN AHL — LIVE`

This document is the sole owner of release-transition derivation, release
prerequisites, release checks, ordering, and deploy or release validation. It
is a live normative owner routed by the newborn AHL.

## Ownership and independence

Release policy derives whether an exact artifact can make an exact transition
to an exact Target Binding. It is independent of factual Level, Boundary,
Authorization, and Recovery. It consumes their results where a release
requirement explicitly depends on them; it does not redefine those owners or
turn their result into a release decision by itself.

Release is not implied by a branch name, repository, path, environment label,
provider, or technical ability to write. The artifact and Target Binding must
each be identified sufficiently for the transition under consideration.

## Artifact to Target Binding transition

The release proposition is:

```text
EXACT ARTIFACT -> EXACT TARGET BINDING -> PLANNED RELEASE TRANSITION
```

The exact artifact identity includes the version or content basis and the
material build or packaging facts needed to distinguish it. The exact Target
Binding identifies the intended target, effect subset, and relevant authority
or environment facts. A repository, branch, path, or environment label alone
is not target identity and cannot establish the transition.

The release result records the artifact, Target Binding, transition, required
preconditions, post-act obligations, observed checks, and remaining
uncertainty. A release result must not silently widen the artifact or binding
after the gate is evaluated.

## Release requirements

Depending on the transition, release requirements may include:

- exact artifact identity and integrity basis;
- exact Target Binding and effect subset;
- required checks and their applicable scope;
- safety-critical ordering constraints;
- prerequisite Evidence, including Recovery, Boundary, or validation
  Evidence owned elsewhere;
- deploy or release validation; and
- post-release Evidence for obligations that can only be observed after the
  Act.

The policy derives the applicable set rather than requiring every conceivable
check for every provider. An omitted requirement must be explainable from the
exact transition; it must not be omitted merely because it is inconvenient.

## Temporal semantics

True preconditions must be established before `PROCEED` and before the Act.
The route must plan every post-act obligation and make its observation and
Evidence reachable before the Act occurs. An obligation that can only be
observed after the Act is not falsely presented as a precondition; it remains
an explicit post-act obligation with a defined validation point and failure
response.

The release gate must not require an impossible precondition, such as Evidence
that cannot exist until after the transition, while also pretending that the
obligation is satisfied before the transition. The distinction between
precondition and post-act obligation is part of the release result.

`UNRUN`, `UNKNOWN`, `NOT OBSERVED`, stale, or inapplicable is not `PASS`.
Only applicable checks with sufficient Evidence can satisfy a required
release condition. A skipped check remains visible with its reason and effect
on the decision.

## Owner result boundaries

Release may consume a factual Level result, Boundary result, Authorization
Envelope or gate result, Recovery applicability or Evidence, Target Binding,
and Work Unit validation. The owning policy continues to define each result:

- consequence policy owns factual Level;
- boundary policy owns Boundary derivation and satisfaction;
- authorization policy owns permission and the Auth Envelope;
- recovery policy owns Recovery Capability and Recovery Evidence;
- `ahl-flow.md` owns Target Binding and Work Unit semantics; and
- this policy owns only the release transition and its temporal requirements.

No release check can grant authority, replace a Boundary, make Recovery Fast,
or create a Target Binding merely by naming one.

## Provider-independent release model

The canonical model is provider-independent. Git, GitHub, pull requests,
continuous integration, snapshots, databases, and production providers are
not canonical release architecture. A provider adapter may observe or enact a
concrete release transition, but it must preserve the generic artifact,
Target Binding, requirement, ordering, validation, and Evidence semantics.

Provider presence is not proof that a release target exists or that a release
requirement passed. Provider-specific observations remain evidence for the
exact proposition they support.

## Failure and stop conditions

The release result exposes the exact unmet requirement, artifact or binding
uncertainty, ordering problem, failed validation, and affected transition.
It does not silently continue, widen scope, or create a global degraded mode.
Conflict, an identity mismatch, an unmet precondition, an unrun required
check, or an unreachable post-act obligation stops the release route until the
owning issue is resolved.
