# NEWBORN WORK UNIT FORMAT — NON-LIVE STAGING

Status: `NEWBORN IMPLEMENTATION — STAGED, NOT LIVE`

This document defines only the durable serialization format for an already
semantic Work Unit. `ahl-flow.md` is the sole owner of Work Unit semantics,
membership, routing, authorization flow, and effect interpretation. This
format is not a runtime database and does not activate the newborn graph.

## Serialization-only boundary

Serialize a Work Unit when a durable, inspectable representation is needed
for handoff, audit, reservation, validation, or another explicit route need.
An ordinary edit does not require a durable artifact merely because it exists.

Serialization records owner results and references; it must not duplicate,
reinterpret, or create the rules that produced them.

The format is intentionally a minimal, readable Markdown/YAML-like contract.
It is one canonical serialization contract. No runtime database is required,
and JSON is not required unless the canonical blueprint later explicitly
requires it.

## Canonical representation

The following shape is normative as a field inventory. Values are references or
facts from the owning policies, not newly defined semantics:

```yaml
work_unit:
  identity: <occurrence identity and Work Unit identity>
  goal:
    reference: <Goal reference>
    contribution: <contribution to the Goal>
  operation: <requested operation>
  route: <selected Route reference>
  scope: <bounded scope>
  effects:
    - target_binding: <per-effect Target Binding reference>
      material_effects: <material effects>
      exclusions: <explicit exclusions>
  dependencies: <descriptive dependencies and required order>
  safety_critical_ordering: <ordering constraints>
  factual_level: <factual Level result reference>
  recovery: <per-use Recovery applicability reference>
  boundary_results: <Boundary result references>
  release_results: <Release result references>
  authorization: <Auth Envelope reference>
  membership: <membership result reference>
  validation_requirements: <validation requirements and result references>
  route_stop_conditions: <Route stop-condition references>
  reservation: <reservation state when applicable>
```

The representation must be able to carry, without silently broadening scope:

- identity and occurrence identity;
- Goal reference and contribution;
- Operation, selected Route, and scope;
- a Target Binding reference for each effect;
- material effects and exclusions;
- dependencies and safety-critical ordering;
- factual Level;
- per-use Recovery applicability reference;
- Boundary result references;
- Release result references;
- Auth Envelope reference;
- membership result;
- validation requirements;
- Route stop conditions; and
- reservation state when applicable.

An absent optional result is represented as absent or not-applicable with its
reason. It is not silently treated as passed, satisfied, authorized, or
complete.

## References, not duplicated rules

Each reference points to the owner result or source that gives it meaning.
The serialized Work Unit may include a human-readable summary for inspection,
but the summary is not a second normative rule. In particular, this format
does not define:

- what a Work Unit means or when it belongs in a Work Unit;
- factual Level or consequence classification;
- Recovery Capability, Fast status, or Recovery Evidence;
- Boundary derivation or satisfaction;
- release transition requirements;
- Authorization or the Auth Envelope; or
- Target Binding semantics.

Those meanings remain with their owners and are referenced here only to make
the already semantic Work Unit durable and auditable.

## Authority and hierarchy

The authority model is flat. A serialized parent does not inherit authority,
approval, Target Binding, Boundary satisfaction, Recovery applicability, or
release readiness from a child; a child does not inherit them from a parent.
Parent, child, and dependency references are descriptive and may express
membership or ordering only. Each Work Unit and each effect remains bound to
its own owner results.

Serialization cannot create permission by nesting a reference or by copying a
successful result from another occurrence. Occurrence identity distinguishes a
new use of the same semantic operation from the earlier use.

## Validation and stop behavior

The format preserves validation requirements, observed results, unknowns,
unrun checks, and Route stop conditions. It must not serialize an unrun or
unknown result as `PASS`, and it must not erase exclusions, residual risk, or
an owner failure for readability.

If a required owner result is missing, stale, contradictory, or out of scope,
the Work Unit remains stoppable and the missing result is visible. Repairing a
serialized Work Unit's state-changing meaning is a new semantic Work Unit,
not a formatting operation.

## Cross-owner audit rule

The flow owns Work Unit semantics and membership. This policy owns only the
field contract above. Recovery, Boundary, Release, consequence, and
Authorization policies remain the sole owners of their respective results.
Provider-specific serialization, a runtime database schema, authority
inheritance, or a second serialization contract is an ownership collision and
must stop the route for review.
