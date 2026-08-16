# NEWBORN RECOVERY POLICY — NON-LIVE STAGING

Status: `NEWBORN IMPLEMENTATION — STAGED, NOT LIVE`

This document is the sole owner of the newborn Recovery Capability model. It
defines the capability structure, Recovery Evidence, per-use applicability,
Fast qualification, composition, and failure semantics. It is not a runtime
authority and does not activate the newborn graph.

## Ownership boundary

This policy owns only recovery capability and recovery evidence. It does not
own or redefine:

- factual Level or consequence classification, which belongs to
  `consequence-policy.md`;
- Authorization, the Auth Envelope, approval, or authority latitude, which
  belongs to `authorization-policy.md` and `ahl-flow.md`;
- Target Binding, Boundary, Release, Work Unit semantics, or serialization;
- provider-specific backup, snapshot, Git, deployment, or database rules.

Recovery can make a restoration proposition legible and testable. It never
grants permission to act, lowers factual Level, satisfies Boundary, or turns
an unrun check into Evidence.

## Recovery Capability

A Recovery Capability is a bounded, evidence-backed description of how an
identified affected unit can be restored to an identified known-good basis.
Every capability has exactly these seven fields:

1. **Environment** — the environment and relevant execution conditions for
   which the capability is claimed.
2. **Restore unit** — the exact unit that will be restored, including its
   identity and scope.
3. **Restore closure** — the explicit set of state, files, dependencies, and
   effects the restore claims to cover, plus material exclusions.
4. **Mechanism** — the concrete replacement, rollback, or other restoration
   mechanism.
5. **Validation** — the checks that establish the restored unit and its
   material dependencies are acceptable.
6. **Material dependencies** — dependencies whose condition can change the
   restoration result, including their relevant versions, state, or
   availability.
7. **Evidence** — the evidence supporting the capability's claims, with
   provenance, scope, time, freshness, and locator sufficient for review.

These are the complete structural fields. There is no `Recovery Level` field
and there is no eighth field. A capability may contain explanatory values
inside a field, but it must not create a second recovery taxonomy or hidden
structural field.

## Recovery Evidence

Recovery Evidence supports an exact proposition about an exact capability,
restore unit, target, source, mechanism, or validation result. Evidence should
make clear what was observed, where and when it was observed, what basis was
used, and how a human can inspect it.

A declared restore closure is a claim about intended coverage, not proof that
the closure is complete. Residual risk, excluded state, uncertainty, and
material dependency differences remain visible. The policy must not normalize
unexplained differences into equivalence or certainty.

Evidence carries only while its material basis remains valid. A change to the
environment, restore unit, closure, mechanism, validation basis, material
dependency, or other fact that the proposition depends on can make the
evidence stale or inapplicable. The capability must then be re-evaluated.

Evidence methods may include observation, validation output, an operator
demonstration, or a drill. A drill is an optional method for acquiring or
strengthening Evidence; it is not a universal ritual and is not required when
other sufficient Evidence establishes the proposition.

## Fast qualification

Recovery is Fast only when all three predicates hold for the use at hand:

```text
FAST = BOUNDED AND DEMONSTRATED AND CURRENTLY APPLICABLE
```

- **BOUNDED** means the environment, restore unit, restore closure, and
  material dependencies are exact enough that the claimed action does not
  silently expand.
- **DEMONSTRATED** means Evidence establishes that the stated mechanism and
  validation can achieve the claimed restoration on the stated basis. A
  declaration alone is not a demonstration.
- **CURRENTLY APPLICABLE** means the same capability, target/source basis,
  dependencies, and material conditions hold for the present use.

If any predicate is absent, uncertain, stale, or contradicted, the recovery
is not Fast. A declared-only closure never qualifies as Fast. The policy may
describe a capability before it is demonstrated; that does not upgrade its
status.

## Per-use applicability

Before relying on a capability for a Work Unit, the use binds all of the
following:

- the exact Recovery Capability reference;
- the exact currently known-good target and source basis;
- the actual effect subset the capability will restore or protect; and
- the current applicability determination for this use.

The actual effect subset may be narrower than the capability's declared
closure. A broader closure must not be inferred from a narrower use. Recovery
reports whether the capability applies; Authorization separately determines
which action, subset, exception, or latitude is permitted.

Per-use binding is not authority. It does not satisfy `APPROVAL_REQUIRED`,
`BOUNDARY_REQUIRED`, or any other authorization blocker, and it cannot make a
technical access path a permission.

## Composition

Multiple recovery units may be composed automatically only when their restore
units, closures, mechanisms, validation, and material dependencies are
independent for the claimed use.

The following require composite Evidence and a composite basis rather than
independent composition:

- overlapping restore units or closures;
- ordering or atomicity constraints;
- a shared invariant;
- coupled state or coupled material dependencies; or
- any interaction that means one restoration can change the proposition for
  another.

Composition must expose the overlap, order, atomicity, coupling, and residual
risk. There is no universal ceremony or blanket assumption that a set of
individually described capabilities is jointly valid.

## Failure and degraded applicability

When a capability fails, becomes stale, or cannot establish its proposition,
the failure is exposed with the affected scope, missing basis, and residual
risk. It is not silently converted into success, Fast status, or an unrelated
global failure.

Authorization may suspend the dependent subset of action or latitude when the
recovery basis is unavailable. That suspension does not revoke or alter
unrelated authority whose own requirements remain satisfied. Recovery itself
does not select that authorization outcome.

Recovery cannot self-authorize repair. A state-changing repair, replacement,
or proof-producing repair is a separate Work Unit with its own Route,
Target Binding, Boundary, Authorization, and validation. Re-demonstrating the
same capability on the same material basis does not require new Human
approval merely because the demonstration was repeated; any changed basis or
changed action is evaluated on its own facts.

## Owner references and audit rules

The flow may consume Recovery Capability, Evidence, Fast status, applicability,
composition, and failure results. Consequence policy supplies factual Level;
authorization policy consumes recovery results for its own gate; boundary and
release policies consume recovery results where their requirements say so.
Those references are consumption, not ownership transfer.

Any document that creates a Recovery Level, grants authority from recovery,
declares a generic Boundary satisfied, or defines serialization rules is a
collision with this or another owner and must stop the route for review.
